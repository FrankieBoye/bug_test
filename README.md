# Customer Service Support Technician Tech Test
Test for CS Support candidates

## Requirements

Allowing for setting up the project, this tech test should take around 2 hours to complete.

1. Find the cause of issues in the application:
* There are three bugs to find
* You are not required to *fix* the bugs, your aim is to __identify__ what is causing them

2. Document your process:
  * What did you notice/find?
  * What are your recommendations?

## Getting Started
These instructions will get the application up and running on your local machine for bug finding purposes.

* Install Ruby [Ways of Installing Ruby](https://www.ruby-lang.org/en/downloads)
* Install Yarn [Ways of Installing Yarn](https://yarnpkg.com/lang/en/docs/install)
* Clone this git repository `git clone git@github.com:smartpension/smart-cs-support-test.git`
* cd into the locally cloned repo `smart-cs-support-test`
* Run `bin/setup`
* Start up your web-server (see the output of `bin/setup`)
 * If you get an error with: `getaddrinfo: nodename nor servname provided, or not known (SocketError)`
   * Try running your server with`./bin/rails server -b 0.0.0.0`

* Navigate to: http://localhost:3000

Remember to document __how__ you identified the bugs and attach your findings to your email back to us, have fun!!


## Findings

#### Bug 1

Playing around with the application, my first observation is that regardless of which 'Show' button is clicked, only the first Company 'Mickeys Plaice' gets displayed.

![image](https://user-images.githubusercontent.com/44870179/84205740-aa32c080-aaa5-11ea-9a25-7cfdab46e097.png)

![image](https://user-images.githubusercontent.com/44870179/84205844-e534f400-aaa5-11ea-9851-e17bf76090dd.png)

A look in the companies_controller.rb file reveals why. If I comment out @company = Company.first on line 11, I can then view the other companies employees.

![image](https://user-images.githubusercontent.com/44870179/84206157-773cfc80-aaa6-11ea-829d-72b27250e41b.png)


#### Bug 2

![image](https://user-images.githubusercontent.com/44870179/84297312-3b0ca900-ab45-11ea-91ca-648a91f3b76f.png)

When trying to add an employee to any company I found I was getting the above error message.

This was harder to rectify so I turned to Google. I found this page which talked about validation.

https://guides.rubyonrails.org/v4.1/active_record_validations.html

Then it was a case of seeing what was expected to be validated and what was actually being validated.

In models/employees.rb the employee class validates :forename, :surname and :middlename.

In views/employess/new.html.erb the form.label for surname had a typo :middlename which would always be empty due as it should say :surname.

![image](https://user-images.githubusercontent.com/44870179/84298353-e66a2d80-ab46-11ea-9f4d-dd10e3f11545.png)

With :middlename changed to surname and :middlename removed from validation in models/employees.rb, the application can have employees added.

![image](https://user-images.githubusercontent.com/44870179/84298551-32b56d80-ab47-11ea-8466-329b6d6f1e78.png)
