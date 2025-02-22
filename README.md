# Subtle KVO Crash with Weak References in Objective-C

This repository demonstrates a subtle bug in Objective-C related to Key-Value Observing (KVO) and weak references.  The bug arises when an observed object is deallocated while a KVO observer is still registered, leading to crashes or unpredictable behavior if the observer attempts to access properties of the deallocated object.

The `bug.m` file contains code that reproduces the issue. The `bugSolution.m` file shows how to fix it by ensuring the observer is removed before the observed object is deallocated.

## How to Reproduce

1. Clone this repository.
2. Open the project in Xcode.
3. Run the application.  You'll likely encounter a crash.
4. Examine `bugSolution.m` to see the solution.

## Solution

The solution involves diligently removing the observer using `removeObserver:forKeyPath:` in appropriate lifecycle methods of your class (e.g., `dealloc`, or when the observed object is no longer needed).  This prevents attempts to access deallocated memory.