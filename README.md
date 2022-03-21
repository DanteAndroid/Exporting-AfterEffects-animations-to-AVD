# Exporting AfterEffects animations to AVD

## What is AVD? Why should I use it?

AVD stands for [AnimatedVectorDrawable](https://developer.android.com/reference/android/graphics/drawable/AnimatedVectorDrawable), it's a well-supported format (like Menu, BottomNavigationView) of drawable which can animate in Android. Besides, animations in AnimatedVectorDrawable can remain smooth even when there is heavy workload on the UI thread.

## I am a designer, what should I do?

If your design resources is `.ai` format (Adobe Illustrator), you can easily export AVD resources by following steps; If not, consider to use AI to create them.

1. Make sure you have installed BodyMovin plugin, if not please install.
2. Import your `.ai` resources to AE and create your animations.
3. Click Window->Extensions->Bodymovin, choose your destination folder, then  click settings, scroll down and select it when you see AVD option, click save. Select your resources, click render, boom! You got a avd folder.
4. Send the avd folder to Android developers of your company, he knows how to use it.

## I am Android developer, what can I do?

1. Ask your UI designer could she make animations with Adobe Illustrator & After Effects?
2. If so, then you can send the tutorial above to her; If not, invite her to dinner and make her reconsider it.
3. When you got AVD fold, which contains resources of your AVD drawable resouces, just copy them to your Android Studio project's drawable folder.
4. You can preview your AVD animation (like `your_avd.xml`) now by click `play` button in preview screen.
5. Create your static vector resource drawable from your_avd.xml. Just copy the vector element under android:drawable attribute and create new drawable file named `avd_resouce_selected.xml`. This drawable is usually used for your icon's selected/checked state.
6. Create your selector resource as following:

```
<?xml version="1.0" encoding="utf-8"?>
<animated-selector xmlns:android="http://schemas.android.com/apk/res/android">
		<!-- This is a vector drawable you create from your AVD xml. -->
    <item
        android:id="@+id/checked"
        android:drawable="@drawable/avd_resouce_selected"
        android:state_selected="true" />
    <!-- This is a static icon provided by your UI designer -->
    <item
        android:id="@+id/unchecked"
        android:drawable="@drawable/icon_resource_default"
        android:state_selected="false" />
    <!-- This is an animation when you select this icon -->
    <transition
        android:drawable="@drawable/avd_party"
        android:fromId="@+id/unchecked"
        android:toId="@+id/checked" />

<!--    <transition-->
 // This is an animation when you unselect this icon
<!--        android:drawable="@drawable/avd_friends"-->
<!--        android:fromId="@+id/checked"-->
<!--        android:toId="@+id/unchecked" />-->
</animated-selector>

```

7. Reference your selector like this:

```
    <item
        android:id="@+id/navigation_home"
        android:icon="@drawable/home_icon_selector"
        android:title="@string/title_home" />
```

