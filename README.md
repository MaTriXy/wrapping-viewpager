# WrappingViewPager
[![jitpack.io][2]][3]
[![Apache License 2.0][4]][5]

ViewPager replacement with dynamic height support and smooth animations for the few edge cases where a standard ViewPager doesn't fulfill your needs.

**This project is inactive. Pull requests are welcome!**

![Sample](https://thumbs.gfycat.com/RealisticBlissfulAdamsstaghornedbeetle-size_restricted.gif) ![Sample 2](https://thumbs.gfycat.com/DeficientBoilingChuckwalla-size_restricted.gif)

## Install

The library is available on [**jitpack.io**][3].

**Gradle dependency:**
```gradle
allprojects {
    repositories {
        maven { url 'https://jitpack.io' }
    }
}
```
```gradle
dependencies {
	compile 'com.github.iffa:wrapping-viewpager:1.10'
}
```

## Quick start

Integrating the library takes less than five minutes: below are the basic steps to get you started.

1. Use `xyz.santeri.wvp.WrappingViewPager` instead of `android.support.v4.view.ViewPager` and set the height to `wrap_content` in your layout file:
 	```xml
  	<xyz.santeri.wvp.WrappingViewPager
    	android:id="@+id/viewpager"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
	```
2. Replace your `PagerAdapter` with any one of the following adapters with wrapping-functionality built-in:
   * `WrappingFragmentPagerAdapter`
   * `WrappingFragmentStatePagerAdapter`

	**OR**
    
   * Implement the wrapping in your own adapter implementation by overriding `PagerAdapter#setPrimaryItem(ViewGroup, int, Object)` like so:
      ```java
      private int mCurrentPosition = -1; // Keep track of the current position

      @Override
      public void setPrimaryItem(ViewGroup container, int position, Object object) {
          super.setPrimaryItem(container, position, object);

          if (!(container instanceof WrappingViewPager)) {
              return; // Do nothing if it's not a compatible ViewPager
          }

          if (position != mCurrentPosition) { // If the position has changed, tell WrappingViewPager
              Fragment fragment = (Fragment) object;
              WrappingViewPager pager = (WrappingViewPager) container;
              if (fragment != null && fragment.getView() != null) {
                  mCurrentPosition = position;
                  pager.onPageChanged(fragment.getView());
              }
          }
      }
      ```

3. *(optional)* Set the animation duration and interpolator to your liking with `WrappingViewPager#setAnimationDuration(long)` (default 100ms) and `WrappingViewPager#setAnimationInterpolator(Interpolator)`.
  
4. **Enjoy!**

For a working demo see the [sample][1] module.

## License

    Copyright (C) 2016 Santeri Elo

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.


[1]: https://github.com/iffa/wrapping-viewpager/tree/master/sample
[2]: https://jitpack.io/v/iffa/wrapping-viewpager.svg
[3]: https://jitpack.io/#iffa/wrapping-viewpager
[4]: https://img.shields.io/badge/license-Apache%202-blue.svg
[5]: https://raw.githubusercontent.com/iffa/wrapping-viewpager/master/LICENSE
