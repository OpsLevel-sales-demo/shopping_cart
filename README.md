# shopping-cart
A shopping cart created using Ruby on Rails.

# Design decisions

The following design decisions were made:

1. The API allows the user to fetch all products at once as specified in the challenge, however, this is extremely inefficient when dealing with large number of products and is also a security concern. If the database contains many products, then a user can crash the server by requesting all products as the server has to fetch and load all the products into memory first before sending the information back to the user. This will also increase latency between the user and the sever as large data must be sent. One way to avoid this is to add pagination where the API can be restricted to return a max number of products (for example 10 products per page) per request forcing the user to send multiple requests to obtain all the products.

2. Currently, after completing the cart checkout, the cart is emptied. This is to simulate a standard e-commerce website where after completing the purchase, you cart goes back to being empty. However, the application will obviously not store any of your previous orders like most e-commerce websites.

3. The API checks if the product is in stock when adding an item to a cart as well as when attempting to checkout just like most e-commerce websites.

4. The shopping cart is currently configured to use the same database for development, test, and production. This is fine for the challenge; however, it is also a security risk and should not be done in production code.

5. The API currently implements basic input validation and error handling; however, more validation should be implemented. Ideally, more research should be done to determine all the possible errors that can be raised by the Ruby/Rails functions being used. 

6. The API attempts to use SQL functions that are considered immune to SQL injection as much as possible. The API also attempts to and use as little user input as possible in the SQL queries. Before retrieving or modifying the database, the API checks if the data exists or not. This will result in extra calls which will reduce performance, however, since the data is small, I believe compromising a bit of performance is worth the added security.

# Prerequisites
- Ruby
- Rails
- MySQL
- Git

# Installation
`$ git clone https://github.com/zaidoon1/shopping-cart.git`

`$ cd shopping-cart`

`$ bundle`

# DB configuration
1. Open the database.yml file located in shopping-cart/config
2. Change the username: and passsword: fields to your mySQL username and password

Note: The default username is testuser and the default password is password<br>
Note 2: Before attempting to load the products into the DB, please ensure the username being used has permissions to create a database, create tables and populate them

# Load products into DB
Go to root directory of the shopping cart project then run the following command:<br>
`$ rake db:drop db:create db:schema:load db:seed`

Note: If you get an "ActiveRecord::EnvironmentMismatchError" then run the following command before running the command above:<br>
`$ RAILS_ENV=development rails db:environment:set`

# Start server
Go to root directory of the shopping cart project then run the following command:<br>
`$ bin/rails s`

# Interacting with the API
There are two easy ways to interact with the API, one is to use Insomnia (https://insomnia.rest/), the other is to use the API documentation below as it allows you test all the routes through a GUI

# View API documentation (using Swagger)

Visit [http://localhost:3000/api/v1/index.html](http://localhost:3000/api/v1/index.html)

# How to run unit tests:
- bin/rails test test/controllers # run all tests from specific directory.
