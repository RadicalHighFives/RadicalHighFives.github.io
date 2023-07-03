---
layout: post
title:  "Integrating Angular with .NET Web API"
date:   2023-06-30 21:03:36 +0530
categories: .NET Angular Docker Bootstrap
---
Angular is built on Typescript. Angular is component base framework for building scalable web applications. It includes a developer tools to assist in building, testing and updating your code. Typescript is opensource and it is a object oriented language whereas javascript is a prototype-based language. Typescript is typed language. This project I created an angular project and .NET core web API project. The angular calls the .NET Core API. I used Azure data studio to connect to a local SQL server database. There isn't a SQL Management version for MAC books so I created a docker container image for the latest 2019 version. .NET Core allows for dependency injection which is techiniques that allows objects/function to receive other objects/functions that depends on it. 


Get request: a repository was created to handle the aysnc methods. Below sample code of the controller.    
```c#
   [HttpGet]
    public async Task<IActionResult> GetAllCustomers()
    {
        var result = await _customerRepository.GetCustomers();
        return Ok(result);
    }
```

Model: Customer model
```c#
using System;
namespace web_api.Models
{
	public class Customer
	{
		public Guid Id { get; set; }
		public string Name { get; set; }
		public string Email { get; set; }
        public long Phone { get; set; }
    }
}
```

Dependency Injection happens in the Program.cs file. 
```c#
var builder = WebApplication.CreateBuilder(args);
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();
builder.Services.AddScoped<ICustomerRepository, CustomerRepository>();
builder.Services.AddScoped<IEmployeeRepository, EmployeeRepository>();
builder.Services.AddDbContext<WebAppDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("ConnectionStr")));
```
