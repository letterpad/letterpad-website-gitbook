# Good Practices

Since Letterpad has a tiny footprint in terms of features, we expect the client to be very performant. The API is agnostic about the client, but when can still allow users to perform css modifications from the Admin Dashboard. This is only possible if your client has syematic markup and appropriate classes that can be used to customise the look and feel.  


#### CSS Frameworks

You may choose any css frameworks for theme development, however give priority to light weight frameworks and dead code elimination.

#### Classnames

Have meaningful class names which can allow users to understand and change the css from Admin Panel. You can check the classname in our [default client](https://demo.letterpad.app) and match accordingly but this is not a hard requirement. 

#### CSS Variables

CSS Variables is a great way of allowing users to change branding colors. Avoid using SASS or LESS variables as they need to be compiled after changing any variables.

#### SEO Optimisation

Letterpad API provides all the information that you need to make your client SEO Optimised. Add appropriate meta tags so that, it is able to generate preview of your site from the url. 

#### Lighthouse Score

The principal goal of Letterpad is to make the clients run rediculously fast. Validate the production bundle of your client in [lighthouse](https://developers.google.com/speed/pagespeed/insights/) and check if the performance score is more than 90%.



