---
layout: post
title: Floating labels are problematic
date: 2038-01-01 09:00:01
categories: js
---

Whenever I tell people about the problems associated with placeholders, they normally respond by telling me about the floating label pattern. Whilst it's novel it's a pattern that has several usability problems. Here's why:

## 1. There is no space for an actual hint

Not all fields require a hint. But for those that do, the floating label pattern is unnecessarily constraining. The floating label begins its life inside the control leaving no space for an additional hint.

## 2. They are hard to read

A floating label is normally small, so that when it animates outside of the field, it takes up a small amount of space. But small text is hard to read.

## 3. They need landing space to fly in to

A floated label needs space to fly in to. Meaning, that if labels were of a usable size (see previous point) there would be no saved space anywa&mdash;just more white space.

Alternatively, we could create space as the label moves into position, but this causes the page to judder creating a disorientating experience in the process.

## 4. The animation is disorientating

For people with visual impairments this sort of animation (which is often janky) is disorientating. And for users who zoom in, the label might float itself offscreen, meaning the user loses context.

## 5. They have poor contrast

A floating label has low contrast to make it look different to a real value. Low contrast text is hard to read. As the label floats out of the field, it will need to change colour to make it look like a label otherwise the text could be completely lost in that state.

## 6. It may be mistaken for a value

People that don’t notice the subtle difference in contrast, will skip the field mistaking it for a value. When this happens, the user continues to submit the form only to be shown an error which is unnecessarily frustrating and time consuming.

## 7. Inconsistent behaviour

As radios, checkboxes and select boxes will have fixed labels (and legends) users will endure an inconsistent form experience. For example, when looking at a textbox the user has to look inside the box for the label. Whereas for a  a select box, the user has to look outside the field.

## 8. The label may get cut off

If the floating label is longer than the size of the field, it will be cut off. By using this pattern we unnecessarily constrain ourselves as to the length of the label itself.

## 9. It's a misuse of the standards

Putting aside for the moment that placeholders themselves are problematic. If you're going to put *something* inside the field, it should be a hint, not the label.

## 10. They require more work

All of this to say that designing and building the floating label pattern is more work. More code brings more to maintain and more problems.

## Summary

A novel floating label won't delight users. At most they delight designers. But of course we design for users, not for ourselves. This pattern is a solution that is desparately looking for a problem.

We should design with familiarity and consistency in-mind whenever possible. Nobody wants to use the forms that we design&mdash;users just want the outcome. There are better and more productive techniques for improving form design.