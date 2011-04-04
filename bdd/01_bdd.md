!SLIDE subsection

# Testing / BDD

!SLIDE bullets

# _The_ BDD language

* RSpec
* Cucumber

Come see my other talk about this :)

!SLIDE bullets

# [Shoulda](https://github.com/thoughtbot/shoulda)

* Macros
* Makes it really easy to spec your models

!SLIDE code

    @@@ Ruby

    describe Foo do

      it { should validate_presence_of :name }
      it { should validate_uniqueness_of :email }
      it { should allow_value('foo').for(:bar) }
      it { should_not allow_value('grr').for(:bar) }

      it { should have_many :zaphods }
    end

!SLIDE code

# Timecop

    @@@ Ruby

    Timecop.freeze(Time.now) do
      @foo.publish!
      @foo.published_at.should == Time.now
    end

    Timecop.return

    Timecop.travel(Time.now + 30.days) do
      @foo.should be_overdue
    end

!SLIDE

# FakeWeb

    @@@ Ruby

    FakeWeb.allow_net_connect = false

    FakeWeb.register_uri(:get, 'SOME_URl', :body => PREPPED_BODY)
    FakeWeb.register_uri(:post, 'SOME_OTHER_URI', :body => ANOTHER_PREPPED_BODY)
    
    service = FooService.new
    service.send()
    service.return_code.should == 1

!SLIDE

# Mocking

* [RSpec-Mocks](https://github.com/rspec/rspec-mocks)
* [Mocha](http://mocha.rubyforge.org/)
* [FlexMock](http://flexmock.rubyforge.org/)
* [RR](https://github.com/btakita/rr)

