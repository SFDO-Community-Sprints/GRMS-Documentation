---
layout: default
title: State Management
parent: Contribution
nav_order: 4
has_children: false
---
# State Management

## Overview
Three [contexts](https://reactjs.org/docs/context.html) are used to manage commonly used states within the mobile app.

1. Localization: global modules to translate messages and labels using [expo-localization](https://docs.expo.dev/versions/latest/sdk/localization/).
2. Auth Context: global variable to toggle between login screen and survey features.
3. Survey Editor Context: global variables to manage editing survey values. The `Survey Editor` screen consists of several types of child components that depend on the field type. The parent screen itself centralizes this context, and when a field worker updates an item value on the screen, the field value is propagated from the child components to the parent screen.

See *[src/context](https://github.com/SFDO-Community-Sprints/GrassrootsMobileSurveyApp/tree/main/src/context)* folder for the full source code.

## Localization Context 
Explanation coming soon

## Auth Context
Explanation coming soon

## Survey Editor Context
Explanation coming soon