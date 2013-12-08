---
layout: post
title: "Avoid a particular rule repetion in SASS"
date: 2012-12-21 21:59:00 +0000
comments: true
categories: 
---
A couple of months ago I came across [this question](http://stackoverflow.com/questions/13056757/avoiding-scss-rule-repetion/) on Stack Overflow, about how to not repeat the `behavior` property (to use with [CSS3PIE](http://css3pie.com/) for IE8 and below) in a selector if this was declared more than once due to the inclusion and use of multiple mixins (for like border-radius, box-shadow, etc).

A couple of days ago, while I was working on a similar case, my issue was not how to avoid the repetition of the properties inside a single selector, but to not repeat it at all in the entire css files. This is my solution.

- - -

Due to:
> IE interprets the URL for the behavior property relative to the source
> HTML document, rather than relative to the CSS file like every other
> CSS property

([more info](http://css3pie.com/documentation/known-issues/#relative-paths)), the url is kept in a variable, to be easily changed according to the project:

    $pie-path: "/myproject/PIE.htc";
    
No prefix needed unless 2.1 Android and below and 3.2 iOS and below or CSS3PIE for IE8 and below so this mixin is not really needed anymore &ndash; [more info](http://generatedcontent.org/post/37949105556/updateyourcss3)

    @mixin border-radius ($val) {
      @each $prefix in '' {
    		#{$prefix}border-radius: $val;
    	}
    	@extend %pie !optional;
    }
    
No prefix needed unless 3 Android and below and 4.3 iOS and below or CSS3PIE for IE8 and below &ndash; [more info](http://generatedcontent.org/post/37949105556/updateyourcss3)

    @mixin box-shadow ($val...) {
    	@each $prefix in -webkit-, '' {
    		#{$prefix}box-shadow: $val;
    	}
    	@extend %pie !optional;
    }

A note about "`!optional`": this flag is to avoid SASS to throw an error if that @extend doesn't work (e.g.: the placeholder is in the .scss file for IE and not in the general one, but the mixin is called by both) &ndash; [more info](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#the__flag)
    
Placeholder selector: at the beginning of the file to allow following rules to override any position/fix property.  
A note about "`position:relative`": it's declared here to fix the z-index issues (disappearing backgrounds/borders/shadows) &ndash; [more info](http://css3pie.com/documentation/known-issues/#z-index).  
Depending on the css and project, this rule can break the layout

    %pie {
    	behavior: url($pie-path);
    	position: relative;
    }
    
    
Usage

    .item1 {
    	@include border-radius(10px);
    }
    .item2 {
    	@include border-radius(5px);
    	@include box-shadow(10px 10px 10px rgba(#000, .3));
    }
    .item3 {
    	@include box-shadow(10px 10px 10px rgba(#F90, .8));
    }

Output

    .item1,
    .item2,
    .item3 {
    	behavior: url("/myproject/PIE.htc");
    	position: relative;
    }
     
    .item1 {
    	border-radius: 10px;
    }
    .item2 {
    	border-radius: 5px;
    	-webkit-box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.3);
    	        box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.3);
    }
    .item3 {
    	-webkit-box-shadow: 10px 10px 10px rgba(255, 153, 0, 0.8);
    	        box-shadow: 10px 10px 10px rgba(255, 153, 0, 0.8);
    }

The behaviour rule is not repeated and the css is more clean, with the properties declared only once, thereby facilitating the separation of styles between IE and non-IE.