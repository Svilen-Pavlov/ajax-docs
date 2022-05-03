---
title: WAI-ARIA Support
page_title: WAI-ARIA Support - RadStepper
description: Check our Web Forms article about WAI-ARIA Support.
slug: stepper/accessibility-and-internationalization/wai-aria-support
tags: wai-aria,support
published: True
position: 3
---

# WAI-ARIA Support

**RadStepper** follows the WAI-ARIA Authoring Practices for implementing the keyboard navigation for its component role.

The Stepper uses the *aria-current="true"* attribute to mark the current **StepperStep** and the *aria-disabled* property to mark the disabled state of each step.

>note An issue with the use of WAI-ARIA in HTML documents is that they don’t validate. When you run a HTML document containing ARIA attributes through the W3C Validator it shows errors in the results for any ARIA attributes. The DOCTYPE declarations do not include any information about the WAI ARIA attributes and you cannot have a valid document which includes elements, attributes, and attribute values, not detailed in its DTD’s.
>


# See Also

 * [WAI-ARIA basic information](https://www.w3.org/WAI/intro/aria)


