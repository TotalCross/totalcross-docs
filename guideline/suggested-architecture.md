# Suggested Architecture

## Overview

This guide is intended for developers who have already completed getting started and have a basic understanding of TotalCross UI components, SQLite, Deploy, and Web Services, and now want to know about the architecture and best practices for building more robust and better quality apps.

If you are not already familiar with the TotalCross framework we strongly recommend you to read the entire previous session \(Learning TotalCross\), beginning with Getting Started.

## The mobile user experience

In most cases, computer applications have a single point of entry into a desktop or quick access to programs, and then run as a single monolithic process. 

Mobile apps, on the other hand, have a more complex structure. A standard mobile app contains several components, including Containers, Windows, services, content providers, and calls to native components such as camera or calls.

And when we are developing multiplatform we still have to think more deeply, remembering the particularities of each Operating System to which we want to make the application available. Although TotalCross already does the trickiest part of generating executables and preserving performance, you also need to think about the structure, modeling and configuration of the App.

## Recommended App Architecture

We've separated some suggestions for the architecture of your app. 

### Why do Design Patterns help with the application's organization?

{% page-ref page="suggested-design-patterns/" %}

### Separation of concepts: What is the best way to create UI interfaces?

{% page-ref page="container-x-window.md" %}

### Positioning

{% page-ref page="relative-positioning/" %}

### Best Practices to improve project maintenance

{% page-ref page="colors-fonts-and-images.md" %}



