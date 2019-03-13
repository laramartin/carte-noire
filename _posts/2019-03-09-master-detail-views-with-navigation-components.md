---
layout:     post
title:      Master-Detail views with Navigation Components
date:       2019-03-09 09:00
author:     Lara Martín
summary:    
categories: programming
tags:
  - Android
  - Android Dev
  - Programming
  - navigation
  - Engineering
---

I researched if the Navigation Architecture Components could be integrated with our own navigation system at work. The navigation of this app was implemented via "pushing and popping" fragments.

One thing I could not find was how to deal with Master-Detail views and Navigation Components. A Master-Detail view is a view that contains a list of items on the side of the layout, and by tapping an item, the detail is shown next to it. These views are mostly used in big devices such as tablets, as they have more space to display more information.

In this article, I will show you how you can have Master-Detail views with Navigation Components, but without going into details on how Navigation Components work. For deep-dives on Navigation Components, I recommend you to [take a course](https://www.pluralsight.com/courses/android-navigation-architecture-components-getting-started), or read these series of [articles](https://medium.com/google-developer-experts/android-navigation-components-part-1-236b2a479d44).

## Sample App

The Sample Application that I will use to explain this, is basically a BottomNavigationView with three “master” screens: Feed, Messages and Profile.

![My Sample App running on a phone device](https://raw.githubusercontent.com/laramartin/laramartin.github.io/master/assets/posts_art/2019-03-09-navigation-master-detail/sample-app-phone.png)

When opening the Profile, the user can navigate deep into Account, Notifications and Settings, and navigate back to the Profile.

When we are using a tablet, we want to display the Profile master screen as seen below. The idea is to have the Profile Fragment screen on the left, and the detail screens on the right. This is what we call the Master-Detail views.

![My Sample App running on a tablet](https://raw.githubusercontent.com/laramartin/laramartin.github.io/master/assets/posts_art/2019-03-09-navigation-master-detail/sample-app-tablet.png)

## Creating The Navigation Graphs

The way we are going to solve this, is by having two navigation graphs.

![Two navigation graphs](https://raw.githubusercontent.com/laramartin/laramartin.github.io/master/assets/posts_art/2019-03-09-navigation-master-detail/two-nav-graphs.png)

The “main” navigation graph, covers the whole application navigation, for both phones and tablets, but with an exception, as we won’t be using the actions that take the user from the Profile to the details screens when using a tablet. More on that later.

![nav_graph_main.xml](https://raw.githubusercontent.com/laramartin/laramartin.github.io/master/assets/posts_art/2019-03-09-navigation-master-detail/nav-graph-main.png)

The “profile” navigation graph contains only the three details screens. This graph is going to be used only on tablet, on the right side of the screen.

![nav_graph_profile.xml](https://raw.githubusercontent.com/laramartin/laramartin.github.io/master/assets/posts_art/2019-03-09-navigation-master-detail/nav-graph-profile.png)

You may have an idea already of how are we going to solve this. On tablets, we are going to have a second `NavHostFragment` which is going to use the `nav_graph_profile.xml`. Let’s see now how to do that.

## How To Handle Tablet Mode

A trick I love to use to easily know if we are on a tablet or a phone is to use a resource value that is going to change depending on the device configuration.

![bools.xml contains the value](https://raw.githubusercontent.com/laramartin/laramartin.github.io/master/assets/posts_art/2019-03-09-navigation-master-detail/bools.png)

1. Create a `bools.xml` file in your values folder.
2. Create a variant of the same file, under `values-sw600dp`, which will be used by “big” devices.

On `values` we will have:

```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <bool name="isTablet">false</bool>
</resources>
``` 

On `values-sw600dp`:

```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <bool name="isTablet">true</bool>
</resources>
```

Now let’s look on how to handle this on the ProfileFragment.

## Loading A Different Layout On Tablet

In our onCreateView we will load a different layout depending on the type of device, we can do that with a snippet like this one:

``` 
val isTablet = context.resources.getBoolean(R.bool.isTablet)

when {
    isTablet -> {
        view = inflater.inflate(R.layout.fragment_profile_land, ...)
        displayMasterDetailLayout(view)
    }
    else -> {
        view = inflater.inflate(R.layout.fragment_profile, ...)
        displaySingleLayout(view)
    }
}
```

The `fragment_profile.xml` layout is very simple, and it only contains three buttons.

![fragment_profile.xml contains the value](https://raw.githubusercontent.com/laramartin/laramartin.github.io/master/assets/posts_art/2019-03-09-navigation-master-detail/phone-layout.png)

The profile fragment_profile_land.xml is a bit more complex:

![fragment_profile_land.xml contains the value](https://raw.githubusercontent.com/laramartin/laramartin.github.io/master/assets/posts_art/2019-03-09-navigation-master-detail/tablet-layout.png)

On the left we have exactly the same layout as we had in the fragment_profile.xml, but on the right, there’s another Fragment with the id `profile_nav_container`, the NavHostFragment (which is previewed as the Account screen).

```
<fragment
        android:id="@+id/profile_nav_container"
        android:name="androidx.navigation.fragment.NavHostFragment"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:defaultNavHost="false"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@id/guideline"
        app:layout_constraintTop_toTopOf="parent"
        **app:navGraph="@navigation/nav_graph_profile"/>**

```

As you can see, the navGraph is the `nav_graph_profile` we defined before, and here is were the Master-Detail navigation will happen.

If we run the project like that, it will look correct both on phone and tablet, but the navigation wouldn’t work yet, because we have to implement it.

## How To Navigate

You noticed before that I had two methods: displaySingleLayout and displayMasterDetailLayout. These methods take care of configuring the navigation on both cases.

Let’s see how:

## TODO!!!

https://gist.github.com/laramartin/020a8529842a4659282a3017c4563a8d#file-displaysinglelayout-kt

<script src="https://gist.github.com/laramartin/020a8529842a4659282a3017c4563a8d.js"></script>

On `displaySingleLayout`, I am just configuring the buttons I have to navigate to the corresponding detail screen. So for example, the `account_textview` is going to navigate to the Account Fragment using the `action_profile_fragment_to_fragment_account` Action.

With the `displayMasterDetailLayout` function is a bit more complicated.

<script src="https://gist.github.com/laramartin/b4d6101412bcedfb09d1f4d5f784ef8a.js"></script>

The idea is to use the `NavHostFragment` we have on the right of the screen to perform navigation, instead of using the one contained in the `MainActivity`.

First, obtain the `NavHostFragment` by calling to the `childFragmentManager.findFragmentById` and then passing the id of the `NavHostFragment`.

Then, instead of using the `createNavigateOnClickListener`, we need to call to navigate manually using the `NavHostFragment` we just got.

## WOW! 🤯

## Summary

Handling tablet navigation can be daunting task, but if we apply the principles of the Navigation Component, we can create our own solutions easily. However, this may not be obvious when looking at the official documentation.

The way I solved this was by having two navigation graphs, and by having two different layouts for my ProfileFragment.

Having more than one navigation graph is completely OK, so don’t be afraid of doing that.

You can find all the code from this article here:

https://github.com/laramartin/android-navigation-master-detail