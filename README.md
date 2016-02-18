Android SwipeableRecyclerView
=====================

Based on [romannurik`s Android-SwipeToDismiss](https://github.com/romannurik/Android-SwipeToDismiss).

Sample project implementation of a list of `CardView`s in a `RecyclerView` with a `TouchListener` that allows dismissing of elements by swiping the elements to the left or right.

![Output sample](https://raw.githubusercontent.com/brnunes/SwipeableRecyclerView/master/demo.gif)

####How to use

- Add these Gradle dependencies to your app's module:

    ````
    dependencies {
        ...
        
        // already includes 'com.android.support:recyclerview-v7:23.1.1'
        compile 'com.github.brnunes:swipeablerecyclerview:1.0.2'

        // only necessary if you are using CardView
        compile 'com.android.support:cardview-v7:23.1.1'
    }
    ````
The `RecyclerView` and `CardView` widgets are part of the [v7 Support Libraries](https://developer.android.com/tools/support-library/features.html#v7).
- Instantiate a `SwipeableRecyclerViewTouchListener` passing as parameters the `RecyclerView` and a `SwipeableRecyclerViewTouchListener.SwipeListener` that will receive the callbacks.
- Add the instantiated `SwipeableRecyclerViewTouchListener` as a [`RecyclerView.OnItemTouchListener`](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.OnItemTouchListener.html).

    ```java
    SwipeableRecyclerViewTouchListener swipeTouchListener =
            new SwipeableRecyclerViewTouchListener(mRecyclerView,
                    new SwipeableRecyclerViewTouchListener.SwipeListener() {
                        @Override
                        public boolean canSwipeLeft(int position) {
                            return true;
                        }

                        @Override
                        public boolean canSwipeRight(int position) {
                            return true;
                        }

                        @Override
                        public void onDismissedBySwipeLeft(RecyclerView recyclerView, int[] reverseSortedPositions) {
                            for (int position : reverseSortedPositions) {
                                mItems.remove(position);
                                mAdapter.notifyItemRemoved(position);
                            }
                            mAdapter.notifyDataSetChanged();
                        }

                        @Override
                        public void onDismissedBySwipeRight(RecyclerView recyclerView, int[] reverseSortedPositions) {
                            for (int position : reverseSortedPositions) {
                                mItems.remove(position);
                                mAdapter.notifyItemRemoved(position);
                            }
                            mAdapter.notifyDataSetChanged();
                        }
                    });

    mRecyclerView.addOnItemTouchListener(swipeTouchListener);
    ````
