## To do
* migrations
* Active Record overview

## Using MySQL
By default, Rails will use SQLite as its model database, but you can easily tell the project generator to use MySQL:

~~~
  $ rails new example -d mysql
~~~

This will create a config/database.yml file containing something like the following:

~~~ yaml
  development:
    adapter: mysql2
    encoding: utf8
    reconnect: false
    database: example_development
    pool: 5
    username: root
    password:
    socket: /var/run/mysqld/mysqld.sock
~~~

The mysql2 gem will need to be installed, but it will have been added to the default Gemfile created by the generator.  Run `bundle install` to update.

The database may then be created:

~~~
  $ rake db:create
~~~

## Seed data
Rails is great out-of-the-box if you want to manually populate a database table using the generated forms.  But that's not always possible if you have a larger chunk of data that you need to upload into a table.  Also, its often desirable to have a canned set of data available for testing purposes.  These data are often referred to as "seed data".  Populating the table with data outside of ActiveRecord is not really recommended for at least several reasons:

* Validation. You'd need to make sure that the database enforces the same validations that you have in your models.
* Timestamps. You'd need to update timestamps manually if you want to keep the `created_at` or `updated_at` attributes current.
* Counter Caches. You'd need to update counts manually.

Rails provides a default location for seed data, the `db/seeds.rb` file.  This file may be modified to contain code to populate tables in the model.  The following example illustrates using this file to load data into a table from an external tab-delimited flatfile (located in vendor/data).  

First build a table, in this case a list of HathiTrust members:

~~~ bash
  $ rails generate scaffold Member member_id:string member_name:string
  $ rake db:migrate
~~~

The following code in the db/seeds.rb file may then be used to populate the table:

~~~ ruby
  Member.delete_all
  f = File.new(Rails.root.join('vendor', 'data', 'Members.seed.tsv'))
  f.each do |member|
    member_id, member_name = member.chomp.split("\t")
    Member.create!(:member_id => member_id, :member_name => member_name)
  end
~~~

Rake the file:

~~~ bash
  $ rake db:seed
~~~ bash

See also:  [RailsCasts seed data](http://railscasts.com/episodes/179-seed-data)


## Active Record Basics

Active Record is the defaul Rails Object-Relational Mapper (ORM).  Fundamentally, each table in the database will have a corresponding class definition which is an instance of `ActiveRecord::Base`. By default, Active Record will assume that the name of the class associated with a table is the singular form of the name of the table (Rails has built-in heuristics for the singlular<->plural mappings of many nouns, which can be overridden if necessary).  Instances of the Active Record class for a table correspond to rows in the table, and these objects have attributes corresponding to columns in the table.

For example, the scaffold generator listed in the section above created a table called `members`, and a class named Member. The class definition is as follows:

`/app/models/member.rb`
~~~ ruby
  class Member < ActiveRecord::Base
    attr_accessible :member_id, :member_name
  end
~~~

The members table itself is defined by the following migration:

`/db/migrate/20121023164711_create_members.rb`
~~~ ruby
  class CreateMembers < ActiveRecord::Migration
    def change
      create_table :members do |t|
        t.string :member_id
        t.string :member_name
        t.timestamps
      end
    end
  end
~~~

Migrations are changes to the data model of an application, encapsulated in ordered source files.  See `migrations` for more info.  

The model can be explored a little bit more closely using the `rails console`:

~~~ ruby
  $ rails console
  > Member.column_names
    => ["id", "member_id", "member_name", "created_at", "updated_at"]
  > Member.columns_hash["member_id"]
    => #<ActiveRecord::ConnectionAdapters::Mysql2Adapter::Column:0xa346e08 @name="member_id", 
    @sql_type="varchar(255)", @null=true, @limit=255, @precision=nil, @scale=nil, @type=:string, 
    @default=nil, @primary=false, @coder=nil, @collation="utf8_unicode_ci"> 
~~~

So this says that there are five columns in the database table for Member.  Looking at the `member_id` column, it can be seen that its a varchar of 255 characters, it can be null, it has no default value, and it isn't the primary key (amongst other things).

Similar information can be found by looking at the table via the mysql command line tool:

~~~
  mysql> describe members;
  +-------------+--------------+------+-----+---------+----------------+
  | Field       | Type         | Null | Key | Default | Extra          |
  +-------------+--------------+------+-----+---------+----------------+
  | id          | int(11)      | NO   | PRI | NULL    | auto_increment |
  | member_id   | varchar(255) | YES  |     | NULL    |                |
  | member_name | varchar(255) | YES  |     | NULL    |                |
  | created_at  | datetime     | NO   |     | NULL    |                |
  | updated_at  | datetime     | NO   |     | NULL    |                |
  +-------------+--------------+------+-----+---------+----------------+
  5 rows in set (0.00 sec)
~~~

Notice that Active Record generated additional columns to the table, beyond what was specified in the original scaffold and in the model definition:

* `id`: By default, Active Record will create an auto-incrementing primary key column with this name.  This can be overridden if necessary.  However, Active Record assumes a single column as a key and does not support composite keys. 
* `created_at`, `updated_at`: These columns contain automatically updated timestamps for the record's creation and last update.
