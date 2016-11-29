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

For register the cell change the following

<pre>[collectionView registerClass:[CustomFSCalendarCell class]forCellWithReuseIdentifier:FSCalendarDefaultCellReuseIdentifier];</pre>

In cellForItemAtIndexPath

<code>    CustomFSCalendarCell *cell = [self.proxy cellForDate:[self.calculator dateForIndexPath:indexPath] atMonthPosition:position];</code>

In didSelectItemAtIndexPath and didDeselectItemAtIndexPath change the cell as customCell

<code>     CustomFSCalendarCell *cell; </code>

for willDisplayCell

<code> [self.proxy willDisplayCell:(CustomFSCalendarCell *)cell forDate:date atMonthPosition:monthPosition];
</code>
