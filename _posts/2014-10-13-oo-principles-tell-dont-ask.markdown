---
layout: post
title:  "OO Principles: Tell, Don't Ask"
date:   2014-10-13 18:42:43
categories: engineering development object-oriented-practises OO
comments: true
---
I first heard “Tell don’t ask” during a course being given by ThoughtWorks and it’s certainly one of a set of phrases and one-liners that run through my head when coding.

I find that a core set of easy to remember principles help govern my coding both during the planning, implementation and refactor and ultimately save me quite a bit of time in the process. One could argue that I’m performing a miniaturised version of Agile in my head, holding a planning session, then performing code reviews before having a retrospective, all in the space of a few minutes.

The main principal behind “Tell, don’t ask” (which I’ll refer to as TDA from now on) is that you should tell your objects what you want them to do, rather than asking them about their state and performing additional callsbased on the answer. This encapsulates the business logic in the correct place and can prevent mutable properties from leaking to external classes where their state can be changed incorrectly, causing a direct and negative effect on the system’s overall state.

Example

The following represents a trivial example, but hopefully it helps to explain the principle in greater detail.

{% highlight c# %}
public class Converter 
{
    private IMap mapper = new XmlResponseMapper();
    
    public bool ConvertFromBase { get; set; }
 
    public MappedObject CreateFrom(Response response) 
    {
        return this.mapper.Map(response);
    }
 
    public MappedObject ConvertFromBase(Response response, MappedObject mappedObject) 
    {
        return mapper.Map(response, mappedObject);
    }
}
{% endhighlight %}

So here we have a simple class that performs conversion to either a fresh instance of an object, or maps properties from the response into an existing object. Nothing too daring. Let’s look at an example of this object’s consumer:

{% highlight c# %}
public class ResponseConsumer 
{
    private Converter converter = new Converter();
    private MappedObject mappedObject;
    public ResponseConsumer(MappedObject mappedObject) {
        this.mappedObject = mappedObject;
    }
 
    public MappedObject handleResponse(Response response) {
        converter.setConvertFromBase(mappedObject != null);
        if (converter.getConvertFromBase()) {
            return converter.convertFromBase(response, this.mappedObject);
        }
 
        return converter.createFrom(response);
    }
}
{% endhighlight %}
This object consumes our convert and based on its own instantiation and state asks the converter if it should convert from base and then calls a different method based on whether the response is true or false. This is awful code and breaks a number of other paradigms in the process, but that only serves to prove the point!

The main focus of this code is the handleResponse method. We tell it to set convertFromBase to a boolean (meaning the class is mutable), then (stupidly, I’ll admit) ask it whether we should convert from base and call convertFromBase if it’s true and createFrom if it’s false. What this code, in effect, is doing is handling the business logic of conversion outside the converter class.

That doesn’t sound right.

So if we were to fix this, how might we do that? Well, for starters, let’s think about the abstraction. We have a response and we want to convert it into an object our system understands. So our class which understands how to handle response should hand off the response, or parts of it, to a class that understands how to convert it. So a single point of entry ‘convert’ would be ideal. Let’s make one! First of all, here’s our response consumer class:

{% highlight c# %}
public class ResponseConsumer 
{
    private Converter converter;
 
    public ResponseConsumer(MappedObject mappedObject) 
    {
        converter = new Converter(mappedObject);
    }
 
    public MappedObject handleResponse(Response response) 
    {
        return converter.convert(response);
    }
}
{% endhighlight %}
We can see this has been greatly reduced in size, with methods down to a single line, including our new ‘convert’ method. Let’s look at the converter class:

{% highlight c# %}
public class Converter 
{
    private final MappedObject mappedObject;
    private IMap mapper = new XmlResponseMapper();
 
    public Converter(MappedObject mappedObject) 
    {
        this.mappedObject = mappedObject;
    }
 
    private boolean getConvertFromBase() 
    {
        return this.mappedObject != null;
    }
 
    private MappedObject createFrom(Response response) 
    {
        return mapper.map(response);
    }
 
    private MappedObject convertFromBase(Response response, MappedObject mappedObject) {
        return mapper.map(response, mappedObject);
    }
 
    public MappedObject convert(Response response) {
        if (getConvertFromBase())
            return convertFromBase(response, mappedObject);
 
        return createFrom(response);
    }
}
This now holds the logic of conversion, encapsulated within one method: convert. This method knows how to convert and knows it very well, handing off to other (now private) methods. The state of this class cannot be changed now either, making it immutable, therefore allowing instances to be more trustworthy.

The secret here was to first consider how we might tell the class what to do, in this case: convert. Once we realise we only have one thing to convert (a Response) then we should create the class according to that. We should tell the converter to convert and let it do all the dirty work.

Summary

I hope this made some sense, especially as it’s my first attempt at this sort of blog post. I also stopped writing it half way through to go on honeymoon so a bit of a refresh had to happen in order to finish it. The main crux is as soon as you spot branches of code using if/else structures, examine the object(s) upon which your if statement relies. If your if statement is asking another object to fulfill the business logic, that is an indicator to extract that into the object in question as a derived property (C#) or a method (java). Tell it to figure out the boolean value instead of asking it!