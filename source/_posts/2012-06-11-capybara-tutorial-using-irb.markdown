---
layout: post
title: "Capybara Tutorial using irb"
date: 2012-06-11 16:03
comments: true
categories: 
---
To get you familiar with capybara, we'll be using irb (Interactive Ruby Shell). 
So before we get started, make sure you have ruby installed. 

Launch irb with the following requirements (ruby, capybara, and capybara/dsl)

    irb -r rubygems -r capybara -r capybara/dsl

Include Cabybara: 

    include Capybara::DSL

Set the default driver.

    Capybara.default_driver = :selenium

Now test that capybara commands work by visiting google

    visit "http://www.gmail.com"

Here's an example for logging into GMAIL
---
    visit "http://www.gmail.com"
    page.has_content?("A Google approach to email.")

    fill_in 'Email', :with => "johnjames4343@gmail.com"
    fill_in 'Passwd', :with => "johnjames4u"
    click_button 'Sign in'