Rails tends to have a pretty strong testing culture and many of the online resources recommend first writing your tests, then your code (Test Driven Development) or a varient of TDD, Behavior Driven Development (BDD). There are different tools/gems used for testing. Here are some common approaches.

## [Rspec](http://rspec.info/)

[Rspec](http://pragprog.com/book/achbd/the-rspec-book) seems to be the most popular Rails test framework.

## [Capybara](https://github.com/jnicklas/capybara) is used to automate certain user tasks (like filling in a web form or performing a file upload with a browser). Capybara is used with other testing frameworks, not stand alone.

Add the rspec and capybara lines to your Gemfile under test (or testing and development as seen below)

~~~ ruby
  group :development, :test do 
    gem 'sqlite3'
    gem 'rspec-rails'
    gem 'ruby-debug19'
  end
~~~

Run `bundle install` to update your gems.

Your testing code should be written in the spec/ directory. There are [quite](http://ruby.railstutorial.org/chapters/static-pages.html#sec-TDD) [a](http://www.ibm.com/developerworks/web/library/wa-rspec/) [few](http://net.tutsplus.com/tutorials/ruby/ruby-for-newbies-testing-with-rspec/) [examples](http://railscasts.com/episodes/71-testing-controllers-with-rspec) on the internet for using Rspec.



## RSpec & Capybara


### Configuring

This section is about RSpec for unit and integration testing using BDD. This is sometimes referred to as “fail-implement-pass”, or even expanded to “red-green-refactor” to include a refactoring stage.

To use RSpec, you need the rspec-rails gem in your Gemfile:

~~~ ruby
group :development, :test do
  gem 'sqlite3', '1.3.5'
  gem 'rspec-rails', '2.11.0'
end
~~~

Additionally, you’ll probably want to add Capybara (for adding web interaction and natural language to your tests):

~~~ ruby
group :test do
  gem 'capybara', '1.1.2'
end
~~~

Next, generate RSpec directory:


~~~ bash
  $ rails generate rspec:install
~~~

To generate integration tests:

~~~ bash
  $ rails generate integration_test name
~~~

Where name might match a controller (or provide some recognizably granular scope). E.g.,

~~~ bash
  $ rails generate integration_test static_pages
~~~

To run this test:

~~~ bash
  $ bundle exec rspec spec/requests/static_pages_spec.rb
~~~


### Things to know...


* describe = context
* it = specify
* let, let!
* expect
* before, after
* pending
* should, should_not (mixed into every object by RSpec; accepts Matcher object)
:Expectation matchers, be_... = be_a_... = be_an_... = have_... = 
::E.g., be_true, be_false, be_nil, be_foo_bar (uses method_missing to call obj.foo_bar?)
:::Custom expectation matchers. Options:
::::1. creating new expectation managers by defining class with matches?, failure_message_for_should, and failure_message_for_should_not (ugh)
::::2. Using custom matcher DSL
::Special Enumerable expectation matchers, include

* subject
* its
* shared_examples_for, it_should_behave_like 
:By convention, stored at: spec/support/shared_examples.rb
* mock, stub


### Examples

The following examples are from Chapter 18 (RSpec) of The Rails 3 Way (Fernandez, 2011).

~~~ ruby
expect {
  BlogPost.create :title => ‘Hello’
}.to change { BlogPost.count }.by(1)

expect {
  blog_post.publish!
}.to change { blog_post.published_on }.from(nil).to(Date.today)

expect {
  blog_post.unpublish!
}.to raise_exception(NotPublishedError, /not yet published/)
describe Array do
  its(:length) { should == 0 } # The implicit subject is Array.new
end

describe BlogPost do
  subject do # Explicit subject
    blog_post = BlogPost.new :title => ‘foo’, :body => ‘bar’
    blog_post.publish!
    blog_post
  end
  it { should be_valid }
  its(:errors) { should be_empty }
  its(:title)  { should == ‘foo’}
  its(:body)   { should == ‘bar’ }
  its(:published_on) { should == Date.today }
end
~~~

Using pending to prevent failing code from failing (interestingly, will cause error if the code no longer causes a failure):

~~~ ruby
pending “implementation of new rating algorithm” do
  BlogPost.new.rating.should == 3.0
end
~~~

Expectation matchers for Enumerable objects:

~~~ ruby
[1, 2, 3].should include(1)
“foobar”.should include(“bar”)
[1, 2, 3].should have(3).items # Yikes.
schedule.should have(3).days   # Syntax sugar => schedule.days.should have(3).items
~~~


### Best practices


The describe and it messages should form a sentence. E.g., the following example generates two sentences:

~~~ ruby
describe “the homepage shows”
  it “register link when not logged in”
  it “account statistics when logged in”
end
~~~

(To check this, run `bundle exec rspec -f d spec/` and verify output reads like a spec document.)
it blocks should contain one test/assertion.


----


### [Cucumber](https://github.com/cucumber/cucumber/wiki) is a little different than rspec in that it has a specific place for user "stories".

Required & suggested gems (to put in the test group in your Gemfile, then run <code>bundle install</code> as usual).

~~~ ruby
  cucumber-rails 
  cucumber-rails-training-wheels 
  database_cleaner
  capybara
  launchy
~~~

To install run

~~~ bash
$ rails generate cucumber:install
~~~

or run 

~~~ bash
  $ rails generate cucumber:install capybara
  $ rails generate cucumber_rails_training_wheels:install
~~~

An essential difference between Rspec and Cucumber is that tests using cucumber are essentially spit into two files. The first file, with a .feature extension is for the 'user story' which is written in [Gherkin](https://github.com/cucumber/cucumber/wiki/Gherkin), a domain specific 'english-like' language. Here's an example of testing a feature in which a user uploads a file, in this case an article, to an online journal. All cucumber tests take place in the features/ directory.

In the file features/article_upload.feature

~~~ cucumber
  Feature: upload an article for a specific journal
    As a user with content
    So that I can add articles to a specific journal
    I want to upload an article file
  Scenario: Uploading a valid docx test file
    Given I am on journal "Journal A" page
    When I upload the test docx file
    Then I should see "Cormac McCarthy, Quantum Copy Editor"
    And I should see "By SCH"
~~~

In the second file, we have the actual tests which just use regexes over the .features file. In file `features/step_definitions/article_steps.rb`

~~~ cucumber
  Given /^(?:|I )am on journal "(.*)" page$/ do |title|
    visit journal_path(Journal.find_by_title( title ).id)
  end
  When /^I upload the test docx file$/ do 
    attach_file("file_upload", File.join(Rails.root, 'features', 'uploaded_files', 'cormacmccarthy.docx'))
    click_button "Submit"
  end
  Then /^(?:|I )should see "([^"]*)"$/ do |text|
    if page.respond_to? :should
      page.should have_content(text)
    else
      assert page.has_content?(text)
    end 
  end
~~~

Cucumber tests are run with `rake cucumber`

----


Cucumber and Rspec are used for different reasons. If you don't know what features you are adding yet, Cucumber might be a good way to go. You can get input from less technical stakeholders to help write your .features before even beginning to write your application code. That's the theory anyway. Maintaining what are essentially two files per test(s) might be problematic, so Rspec might be the winner. It's considered ok to mix both Cucumber and Rspec in your test code, to have tests in both features/ and spec/ depending on what kind of tests you need.

