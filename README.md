Android SwipeableRecyclerView
=====================

Based on [romannurik`s Android-SwipeToDismiss](https://github.com/romannurik/Android-SwipeToDismiss).

Sample project implementation of a `RecyclerView` with a `TouchListener` that allows dismissing of elements by swiping the elements to the left or right.

####How to use:
- Copy the class [`SwipeableRecyclerViewTouchListener`](https://github.com/brnunes/SwipeableRecyclerView/blob/master/app/src/main/java/brnunes/swipeablecardview/SwipeableRecyclerViewTouchListener.java) to your project.
- Instantiate a `SwipeableRecyclerViewTouchListener` passing as parameters the `RecyclerView` and a `SwipeListener` that will receive the callbacks.
- Add the instantiated `SwipeableRecyclerViewTouchListener` as a [`RecyclerView.OnItemTouchListener`](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.OnItemTouchListener.html).


```java
SwipeableRecyclerViewTouchListener swipeTouchListener =
        new SwipeableRecyclerViewTouchListener(mRecyclerView,
                new SwipeableRecyclerViewTouchListener.SwipeListener() {
                    @Override
                    public boolean canSwipe(int position) {
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

