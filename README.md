#  Added Custom Classes:
CustomFSCalenderCell as extending FSCalenderCell.

CustomFSCalendarDelegateProxy as extending FSCalendarDelegateProxy.

Import and use FSCalendarDelegateProxy in FSCalender and FSCalenderDynamicHeader.

Import and use FSCalenderCell in FSCalender and FSCalenderDelegateProxy.

# FSCalender.m 
Import CustomFSCalenderCell.h

change the following method CalenderCell to CustomFSCalenderCell

<code>- (void)invalidateAppearanceForCell:(CustomFSCalendarCell *)cell forDate:(NSDate *)date;</code>

<code>- (NSDate *)dateForCell:(CustomFSCalendarCell *)cell</code>

<code>- (FSCalendarMonthPosition)monthPositionForCell:(CustomFSCalendarCell *)cell</code>

<code>- (NSArray CustomFSCalendarCell * *)visibleCells</code> 

<code>- (void)invalidateAppearanceForCell:(CustomFSCalendarCell *)cell forDate:(NSDate *)date</code>

<code>- (void)reloadDataForCell:(CustomFSCalendarCell *)cell atIndexPath:(NSIndexPath *)indexPath</code>


For register the cell change the following

<pre>[collectionView registerClass:[CustomFSCalendarCell class]forCellWithReuseIdentifier:FSCalendarDefaultCellReuseIdentifier];</pre>

In cellForItemAtIndexPath

<code>    CustomFSCalendarCell *cell = [self.proxy cellForDate:[self.calculator dateForIndexPath:indexPath] atMonthPosition:position];</code>

In didSelectItemAtIndexPath and didDeselectItemAtIndexPath change the cell as customCell

<code>     CustomFSCalendarCell *cell; </code>

For willDisplayCell

<code> [self.proxy willDisplayCell:(CustomFSCalendarCell *)cell forDate:date atMonthPosition:monthPosition];
</code>

For cellForDate atMonthPosition method change the return type

<code>    return (CustomFSCalendarCell *)[self.collectionView cellForItemAtIndexPath:indexPath];
</code>

For deselectDate method 

<code>        CustomFSCalendarCell *cell = (CustomFSCalendarCell *)[_collectionView cellForItemAtIndexPath:indexPath];
</code>

In reloadVisibleCells

<code>        CustomFSCalendarCell *cell = (CustomFSCalendarCell *)[self.collectionView cellForItemAtIndexPath:indexPath];
</code>

For selectCounterpartDate and deselectCounterpartDate create cell as CustomFSCalendarCell

<code>    CustomFSCalendarCell *cell;</code>

#FSCalendarDelegateProxy.h

Change the following methods 

<code>- (CustomFSCalendarCell *)cellForDate:(NSDate *)date atMonthPosition:(FSCalendarMonthPosition)position;
</code>

<code>- (void)willDisplayCell:(CustomFSCalendarCell *)cell forDate:(NSDate *)date atMonthPosition:(FSCalendarMonthPosition)position;</code>
