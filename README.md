[![](https://jitpack.io/v/matecode/DataFragment.svg)](https://jitpack.io/#matecode/DataFragment)
[![API](https://img.shields.io/badge/API-9%2B-blue.svg?style=flat)](https://android-arsenal.com/api?level=9)

# DataFragment

DataFragment is a tiny tiny library that helps (me) to prevent a little boilerplate code for retained data fragments in Android. This is really useful for holding data and longrunning tasks over activity lifecycle, namely orientation changes.
If you want to read more about this topic or have no idea what i'm talking about, read [this](https://developer.android.com/guide/topics/resources/runtime-changes.html#RetainingAnObject)

## Usage

### DataFragment only works with support library fragments !!!

#### Create your DataFragment

For that you have to inherit your class from `DataFragmentBase`. That's all.

[Example](https://github.com/matecode/DataFragment/blob/develop/app/src/main/java/de/mateware/datafragmentsample/DataFragment.java)

Now you can use it in your activity or where ever. You have to possibilities:

#### Activity (simpler, nicer)

You can inherit your Activity from the `DataFragmentActivity`. This will do most of work for you.
All you have to do is three steps:

Extend from DataFragmentActivity with your DataFragment type ...
```
...
public class YourActivity extends DataFragmentActivity<YourDataFragment>
...
```

then put your DataFrament class in the constructor of the class
```
...
    public YourActivity() {
        super(YourDataFragment.class);
    }
...
```

and last use your data with the following methods:

`getDataFragment()` returns your dataFragment. If its not existent yet it will be created or retained. Now you can manipulate with you own methods.

#### Static methods (if you can't extends the Activity)

With this approach you have to keep the fragment yourself. You can get it with the following methods as static methods from your DataFragment:

YourDataFragment.`createOrRetainDataFragment(FragmentManager, YourDataFragment.class)`

YourDataFragment.`createDataFragment(FragmentManager, YourDataFragment.class)`

YourDataFragment.`retainDataFragment(FragmentManager, YourDataFragment.class)`

## Important to know:

:heavy_exclamation_mark: **DataFragment only works with support library fragments !!!**

:heavy_exclamation_mark: **DataFragment uses the (new) [commitNow()](https://developer.android.com/reference/android/support/v4/app/FragmentTransaction.html#commitNow()) to create your data frament, which means its synchronous, but you can use getContext() immediately in your data fragment methods.**

## Installation

DataFragment is published via Jitpack. Add this in your root `build.gradle` file (**not** your module `build.gradle` file):

```gradle
allprojects {
    repositories {
        ...
        maven { url "https://jitpack.io" }
    }
}
```

Add this to your module's `build.gradle` file (make sure the version matches the JitPack badge above):

```gradle
dependencies {
    ...
    compile 'com.github.matecode:DataFragment:1.0.3'
}
```

## Licence

```
Copyright 2017 Mate Siede

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```