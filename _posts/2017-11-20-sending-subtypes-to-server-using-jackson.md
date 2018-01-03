---
layout: post
title:  "Using Jackson to send object subtypes"
date:   2017-11-20 14:13:53 +0200
categories: development
comments: true
lang: en
ref: serialization
---

The following post will be a little 'techie' but I will try to keep it simple even if you have not a technical background. I'd like to explain how I achieve to send serialized objects to a server using jaxrs, jackson and resteasy. 

The first thing to understand is, what it's an object and a class in the software world. Imagine that we want to represent a concept from the world inside an application that we are building. We have to define it with a class that could be for example a Car. This Car it's defined by it's attributes (characteristics) like price, color, kilometers, plate, id ... then in our application we can have many instances of it that we call objects (car1, car2, car3 ...) that each one have their own characteristics. 

We realize that we can group cars by certain characteristics for example by the type of engine: Fuel, Hybrid and Electric. 
Then we can create 3 subtypes of class Car that are: 

- FuelCar
- HybridCar
- ElectricCar  

In the application we can create objects of those new subclasses. Toyota hybrid can be an instance of HybridCar, Citroen C3 an instance of FuelCar ... etc 

In the internet world clients and servers exchange data over the network. The clients request information to servers. Everytime that you go to a website your browser is the client, and the website that you visit acts as a server and sends you the pages that you read in your browser. 

This is the well-known <a href="https://en.wikipedia.org/wiki/Client%E2%80%93server_model">client-server</a> model. In the server instead of a website with html, javascript and css we can have what it's called webservice. A webservice is a software that lives in a server, that has a list of operations available that the clients can invoke and obtain results. If we follow the example of the Cars we can have a webservice that has some operations like: 

- createCar(Car car) 
- getCarById(int id)
- updateCar(Car car)
- deleteCar(int id)
- getCars() 

In this case we have 5 operations where each one has his purpose. To send information between client and server there are different ways of doing it. One of them is through JSON that it's an open-standard file format that uses human-readable text to transmit data objects consisting on attribute-value pairs. For example when we call the operation getCars we get the following JSON:

{% highlight json %}
[{
	id: 1
	price: 1000
	color: blue
	brand: mercedes
	kilometers: 0
	plate: 6574KBE
},
{
	id: 2
	price: 2000
	color: red
	brand: seat
	kilometers: 1000
	plate: 2524IBE
}]
{% endhighlight %}

This kind of REST service can be implemented using a technology called Resteasy that is an implementation of a Java standard whose name is JAX-RS. Resteasy comes with the well known application server called JBoss and it can help you when building REST services. 

Then, how can we serialize the objects that represent our car instances to be sent from the client to the server? There is a library called Jackson that can help you to do the serialization of those objects.

{% highlight java %}

@JsonTypeInfo(use = Id.NAME, include = As.PROPERTY, property = "type")
@JsonSubTypes({@JsonSubTypes.Type(value = FuelCar.class, name = "FuelCar"),
                @JsonSubTypes.Type(value = HybridCar.class, name = "HybridCar"),
                @JsonSubTypes.Type(value = ElectricCar.class, name = "ElectricCar"})
public abstract class Car {	
	private long id;
	private int price;
	private Color color;
	private Brand brand;
	private int kilometers;
	private String plate;
}      

public class FuelCar extends Car {
	//fields defining FuelCar
}


public class HybridCar extends Car {
	//fields defining HybridCar
}


public class ElectricCar extends Car {
    //fields defining ElectricCar	
}

{% endhighlight %}

Then our JSON to send from the client to the server should have the types associated with each object.

{% highlight java %}

[ electricCar : {
	id: 1
	price: 1000
	color: blue
	brand: mercedes
	kilometers: 0
	plate: 6574KBE
},
 hybridCar : {
	id: 2
	price: 2000
	color: red
	brand: seat
	kilometers: 1000
	plate: 2524IBE
},
fuelCar : {
	id: 3
	price: 2000
	color: red
	brand: seat
	kilometers: 1000
	plate: 2524IBE
}

]
{% endhighlight %}


