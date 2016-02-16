---
layout: post
title: Jquery-Turbolinks
---

I had an issue with a past rails project, [Sea Dogs](https://github.com/stevenrayesky/pirate_ships_project), where on initial page load my javascript was not working. On click, I giant message was supposed to flash on the screen to let the user know that they had successfully "stalked" a boat. Unfortunately, it only worked when the page was then reloaded.

Turbolinks is a gem that is on by default in rails. From the turbolinks github:

```
Turbolinks makes following links in your web application 
faster. Instead of letting the browser recompile the 
JavaScript and CSS between each page change, it keeps the 
current page instance alive and replaces only the body 
(or parts of) and the title in the head. 
Think CGI vs persistent process.
```
Faster pages. Pretty cool, right? 

Well, in my case things got a little screwy when mixed with Jquery. Let's see if I can make sense of it:

On a page, I add a click handler to a link with jQuery. It looks like this:

```
$(document).ready(function(){
	$(".boat_image").click(function(){
		$(this).siblings(".expedition_form_div").css("display", "inline");
	});
});
```

Looks ok, right? Only problem is with Turbolinks, the document becomes "ready" once, at first page load. After that, Turbolinks is going around that and only replacing the body. So all of my `.boat_image` links that happen to be on the page at first load get handled the way I want. But any `.boat_image` links on follow-up pages—pages loaded with Turbolinks—never get this click handler added to them. Because `$(document).ready` only fires once, when the page first loads, not after Turbolinks swaps in new content.

In order to fix this I required another gem that fixes this specific problem, [Jquery-Turbolinks](https://rubygems.org/gems/jquery-turbolinks).

3 easy steps to get it working:

1. Put turbolinks in the Gemfile

    ![Jquery-Turbolinks_Gemfile](../../images/Jquery_Turbolinks_Gemfile.png)

2. In your application.js file in your Javascript folder require it. Note the order, it is relevant.

    ![Jquery_Turbolinks_app_js](../../images/Jquery_Turbolinks_app_js.png)

3. Finally 
`gem install jquery-turbolinks` 
and you should be all set!
