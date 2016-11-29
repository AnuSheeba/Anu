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
<code>- (NSArray<CustomFSCalendarCell *> *)visibleCells</code> 

For register the cell change the following
<code>[collectionView registerClass:[CustomFSCalendarCell class] forCellWithReuseIdentifier:FSCalendarDefaultCellReuseIdentifier];</code>
