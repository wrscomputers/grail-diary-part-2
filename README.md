
#### In `AddPOIViewController.swift`:

12. Declare `IBOutlet` properties for the 5 textfields in this view; wire these up to their appropriate textfields in the storyboard
13. Declare a protocol above this class in the same file called `AddPOIDelegate`; declare a single function requirement called `poiWasAdded(_ poi: POI)`
14. Declare a variable property called `delegate` of type `AddPOIDelegate` and make it optional
15. Create 2 `IBAction` methods: `cancelTapped(_ sender: UIBarButtonItem)`, and `saveTapped(_ sender: UIBarButtonItem)`; wire them up to their appropriate bar button items in the storyboard
16. Inside `cancelTapped`, simply dismiss this view as the user has indicated they want to leave this screen
17. Inside `saveTapped`, guard unwrap the text inside the location and country textfields, initialize a `POI` object, and then if-let unwrap the 3 clue textfields and add them to the POI if applicable
18. At the end of the `saveTapped` method, call the delegate method on the delegate property and pass the POI that was just created as an argument
19. In an extension, make the class conform to the `UITextFieldDelegate` protocol
20. In the storyboard, for each textfield in this view, connect the delegate property of the textfield to this class
21. Implement the delegate method `textFieldShouldReturn(_:)`; unwrap the text and make sure it's not empty, then `switch` off the textfield to determine which one called this method; change the `firstResponder` status to the appropriate textfield

#### In `POIsTableViewController.swift`:

22. In an extension, make the class conform to the `AddPOIDelegate` protocol
23. Implement the delegate method `poiWasCreated(_:)`
24. Append the poi that was passed into the method to your array
25. Dismiss the view so the modal animates offscreen
26. Reload the tableview's data
27. In the main class definition, implement the `prepare(for:sender:)` method (it might be commented out)
28. Check the identifier of the segue first; look for the identifier `AddPOIModalSegue`
29. If that identifier is found, use the segue object's `destination` property to grab the view controller we're transitioning to and cast it as an instance of `AddPOIViewController`; you'll need to unwrap this as the cast may not succeed
30. If the unwrap is successful, use the view controller you unwrapped, set its `delegate` property to `self`; this ensures the `POIsTableViewController` will act on behalf of the `AddPOIViewController`

#### In `POITableViewCell.swift`:

31. Declare `IBOutlet` properties for the following cell elements: `locationLabel`, `countryLabel`, and `cluesCountLabel`; connect them to their appropriate labels in the storyboard
32. Declare an optional property called `poi` of type `POI`; add a `didSet` observer that calls a function named `updateViews`
33. Define a private function named `updateViews`; inside, unwrap `poi` and use its properties to populate the various labels with data

#### In `POIDetailViewController.swift`:

34. Declare 3 `IBOutlet` properties: `locationLabel`, `countryLabel`, and `cluesTextView` using `UILabel` and `UITextView` for the types; wire them to their appropriate subviews in the storyboard
35. Declare a variable property called `poi` of type `POI`
36. Create a private method called `updateViews` that takes no arguments
37. Call the above method inside `viewDidLoad`
38. In `updateViews`, unwrap the poi property with `guard` and set the various model properties to the text of the labels and the textview; you'll have to do a little formatting to show the clues as a list in the `cluesTextView`

#### In `POIsTableViewController.swift`:

39. In the `prepare(for:sender:)` method, add an `else-if` to your existing code to check for a different segue identifier, `ShowPOIDetailSegue`
40. If that identifier is found, unwrap the selected row's index path from the tableview, and then grab the segue's destination view controller and cast it as an instance of `POIDetailViewController` (do these two steps together in a compound `if-let`)
41. If those unwraps are successful, set the detail view controller's `poi` property to the appropriate `POI` from the array you use in this class to track all POIs

### Testing

At this point, the app should run and allow new POIs to be entered. They should appear in the main tableview and when tapped, the app should transition to a detail view to show the rest of the information about each POI.
