---
layout: post
title: "WebDriver: Making the switch to ChromeDriver"
date: 2012-07-11 00:05
comments: false
categories: 
---

On my previous project I used Cucumber on top of Capybara to driver out WebDriver. We were initially going to use ChromeDriver instead of the default FireFox ... but I decided at the last minute to stick with Firefox.

Recently, I heard rumors that ChromeDriver is "Faster" than Firefox. So, like the curious person that I am, I decided to switch out FireFox for ChromeDriver to test out this claim. 

### Setting up Cucumber to use ChromeDriver

To make the switch, all I had to do was replace the driver definition from:
	Capybara.current_driver = :selenium	
to:
	Capybara.register_driver :chrome do |app|
	    Capybara::Selenium::Driver.new(app, :browser => :chrome)
	  end
	Capybara.javascript_driver = :chrome

Then in all my Cucumber feature files, I added the tag @javascript:

### Re-run Cucumber Feature Files

When I re-ran my Cucumber Features files using ChromeDriver, I however came across a few errors:
	
	focusElement execution failed;
       Failed to send keys because cannot focus element (Selenium::WebDriver::Error::UnknownError)

> Apparently, You can't use send_keys for certain types of inputs. (Workaround - click the element and then use the advanced interactions API to send keys without an element.) 
	
	Element is not clickable at point (928, 23.5). Other element would receive the click
	
> ChromeDriver always clicks the middle of the element in attempt to be faithful to what an actual user does.
There are two ways to handle this currently:

> * Change/fix the page so that the user can click on the link in the middle.
> * Use the advanced user interactions API to click at the appropriate place in the link. e.g., ActionChains(w).move_to_element_with_offset(link, 0, 20).click().perform()

### Speed Test Results: Firefox vs ChromeDriver

After fixing the issues above and passing all my tests, I was able to compare their speeds and found that ChromeDriver was 15 - 20% faster than Firefox. With a smaller testsuite, the difference might not make much of a difference but can you imagine the difference on a larger testsuite! In the end ... you have to consider whether Chrome's speedy performance is worth dealing with the issues that seem to be ChromeDriver specific. 