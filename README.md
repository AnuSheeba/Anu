#  Added Custom Classes:
CustomFSCalenderCell as extending FSCalenderCell.

CustomFSCalendarDelegateProxy as extending FSCalendarDelegateProxy.

Import and use FSCalendarDelegateProxy in FSCalender and FSCalenderDynamicHeader.

Import and use FSCalenderCell in FSCalender and FSCalenderDelegateProxy.

#FSCalender.h

import CustomFSCalenderCell

Add the following methods

<code>- (nullable NSArrayNSDictionary *  *)calendar:(FSCalendar *)calendar subtitleForDateAsDict:(NSDate *)date;</code>

<code>- (void)didSelectFirstDateCalendar:(NSDate*)selectedDate;</code>

<code>- (void)didSelectSecondDateCalendar:(NSDate*)selectedDate;</code>

<code>- (void)didSelectThirdDateCalendar:(NSDate*)selectedDate;</code>

<code>- (void)didSelectForthDateCalendar:(NSDate*)selectedDate;</code>

<code>- (void)reloadDataForCell:(FSCalendarCell *)cell atIndexPath:(NSIndexPath *)indexPath;</code>

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

<code>cell.fsCalGlobalObj=self;</code>


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

add the Deleage method

<code>- (NSArray NSDictionary *)subtitleForDateAsDict:(NSDate *)date;</code>
#FSCalendarDelegateProxy.m

change the following method as below


<pre>- (CustomFSCalendarCell *)cellForDate:(NSDate *)date atMonthPosition:(FSCalendarMonthPosition)position
{
    if (self.dataSource && [self.dataSource respondsToSelector:@selector(calendar:cellForDate:atMonthPosition:)]) {
        CustomFSCalendarCell *cell = [self.dataSource calendar:self.calendar cellForDate:date atMonthPosition:position];
        if (cell && ![cell isKindOfClass:[CustomFSCalendarCell class]]) {
            [NSException raise:@"You must return a valid cell in calendar:cellForDate:atMonthPosition:" format:@""];
        }
        return cell;
    }
    return nil;
}</pre>


<code>- (void)willDisplayCell:(CustomFSCalendarCell *)cell forDate:(NSDate *)date atMonthPosition:(FSCalendarMonthPosition)position</code>

For preferredRowHeight
<pre>if (UI_USER_INTERFACE_IDIOM() == UIUserInterfaceIdiomPad) {
        return 110;
    }
    return 50;
    </pre>
    
    
# FSCalendarCell.h

change the string type to array of Dictionary

<code>@property (strong, nonatomic) NSArray NSDictionary  *subtitle;</code>

change the property of placeholder

<code>@property (readonly, nonatomic,getter=isPlaceholder) BOOL placeholder;</code>

# FSCalendarCell.m

change the following method

<pre>
- (void)setSubtitle:(NSArray NSDictionary *)subtitle
{
    _subtitle = subtitle;
    [self setNeedsLayout];
}</pre>

#FSCalendarConstants.h

change the color code

<code>#define FSCalendarStandardSelectionColor   FSColorRGBA(31,119,219,1.0)</code>


#FSCalendarConstants.m

change the following values

<code>CGFloat const FSCalendarStandardMonthlyPageHeight = 330.0;</code>

<code>CGFloat const FSCalendarStandardCellDiameter = 30/3.0;</code>

<code>CGFloat const FSCalendarStandardTitleTextSize = 14;</code>

<code>CGFloat const FSCalendarStandardWeekdayTextSize = 18;</code>

<code>CGFloat const FSCalendarStandardHeaderTextSize = 22;</code>


#FSCalendarDynamicHeader.h

<code> #import "CustomFSCalendarDelegateProxy.h"</code>

#FSCalendarAppearance.h

Append the below to init method
 <pre>if (UI_USER_INTERFACE_IDIOM() == UIUserInterfaceIdiomPad) {
            _backgroundColors[@(FSCalendarCellStateSelected)]    =FSCalendarStandardSeparatorColor;
            _subtitleColors[@(FSCalendarCellStateToday)]       = [UIColor whiteColor];//
            _subtitleColors[@(FSCalendarCellStateSelected)]    = [UIColor whiteColor];//Anu changed whiteColor

        }else{
            _backgroundColors[@(FSCalendarCellStateSelected)]    =FSCalendarStandardSelectionColor;
            _subtitleColors[@(FSCalendarCellStateToday)]       = [UIColor whiteColor];//
            _subtitleColors[@(FSCalendarCellStateSelected)]    = [UIColor whiteColor];//Anu changed whiteColor

        }
</pre>

Change the below vaues for iphone and ipad
 <pre>
 - (UIFont *)preferredTitleFont
{
    return [UIFont fontWithName:_titleFontName size:16];
}

- (UIFont *)preferredSubtitleFont
{
    if (UI_USER_INTERFACE_IDIOM() == UIUserInterfaceIdiomPad) {
        return [UIFont fontWithName:_weekdayFontName size:15];
    }
    return [UIFont fontWithName:_weekdayFontName size:10];
}

- (UIFont *)preferredWeekdayFont
{
    
    if (UI_USER_INTERFACE_IDIOM() == UIUserInterfaceIdiomPad) {
        return [UIFont fontWithName:_weekdayFontName size:15];
    }
    return [UIFont fontWithName:_weekdayFontName size:10];
}
</pre>
