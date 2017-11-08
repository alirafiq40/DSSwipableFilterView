# DSSwipableFilterView

<img src="preview.gif" width="230" height="408" />

Snapchat like swipeable filter view in pure swift.

Doesn't matter if you want to apply directly to live camera or static image. Simple pass the UIImage/CIImage to the fuction provided.  Both examples are provided.


## CocoaPods

Suport over CocoaPods is coming next.


## Manual install

Simply drag and drop the **DSSwipableFilterView** folder inside your project in xCode and you are good to go. The library is writen in Swift so if you want to use it in Objective-C project you would need to have the "ProjectName-Swift.h" file autogenerated by xCode for you.


## Usage

After adding the library to your poject open up your viewcontroller and first inicialize the array of filters that you want to use

```Swift
let filterList = [DSFilter(name: "No Filter", type: .ciFilter),
                  DSFilter(name: "CIPhotoEffectMono", type: .ciFilter),
                  DSFilter(name: "CIPhotoEffectChrome", type: .ciFilter),
                  DSFilter(name: "CIPhotoEffectTransfer", type: .ciFilter),
                  DSFilter(name: "CIPhotoEffectInstant", type: .ciFilter),
                  DSFilter(name: "CIPhotoEffectNoir", type: .ciFilter),
                  DSFilter(name: "CIPhotoEffectProcess", type: .ciFilter),
                  DSFilter(name: "CIPhotoEffectTonal", type: .ciFilter)]
```

### DSFilter

DSFilter is providing few inicializers and they are with **Name** and **Type** or you can pass already created **CIFilter** directly. For now the usage of Types other then **ciFilter** and **combinedFilters**  is not yet done.

Initialize with Name and Type
```Swift
let dsFilter = DSFilter(name: "No Filter", type: .ciFilter),
```
Initialize with CIFilter and Type
```Swift
let filter = CIFilter(name: "CIPhotoEffectChrome")!
let dsFilter = DSFilter(name: "DirectFilter", filter: filter, type: .ciFilter)
```
Initialize with Name and CIFIlter, here the type will be set to `.ciFilter` by default
```Swift
let filter = CIFilter(name: "CIPhotoEffectChrome")!
let dsFilter = DSFilter(name: "Filter", filter: filter)
```
This class also supports combination of Two CIFilters, just pass array of two CIFIlters to the init and you are good to go. More then Two coming in the next versions.

```Swift
let filterOne = CIFilter(name: "CIPhotoEffectChrome")!
let filterTwo = CIFilter(name: "CIPhotoEffectProcess")!

let dsCombinedFilter = DSFilter(combinedFilter: [filterOne, filterTwo])
```
**Please use "No Filter" as a name when you want to add No filters to the image**

### DSSwipableFilterView

Next after you have prepared your list of DSFilters you need to prepare the DSSwipableFilterView. Simply add it in your Storyboard, Xib or create it manualy from code with preferred frame or constraints.

```Swift
let filterSwipeView = DSSwipableFilterView(frame: UIScreen.main.bounds)
```
After allocating your view next is to set some properties:
```Swift
filterSwipeView.dataSource = self
filterSwipeView.isUserInteractionEnabled = true
filterSwipeView.isMultipleTouchEnabled = true
filterSwipeView.isExclusiveTouch = false

self.view.addSubview(filterSwipeView) // only if you are adding via code
filterSwipeView.reloadData()
```
DSSwipableFilterView provides protocol which has three functions which you need to implement:
```Swift
// pass the number of filters that you have in your array of DSFilter
func numberOfFilters(_ filterView: DSSwipableFilterView) -> Int

//return the DSFilter at the given index
func filter(_ filterView: DSSwipableFilterView, filterAtIndex index: Int) -> DSFilter

//return the index of which you want to start
func startAtIndex(_ filterView: DSSwipableFilterView) -> Int
```

DSSwipableFilterView provides public functions for passing the image that you want to filter, currently supports CIImage and UIImage. When you have your image ready for presentation simply call:
```Swift
let uiImage = .... get your image
filterSwipeView.setRenderImage(image: uiImage)
```

**If you are adding video from library please use the `isPlayingLibraryVideo` property and set it to `true` or `false` for everything else.**

Thats it you are good to go!

Exporting filtered UIImage is also supported just call the public function on DSSwipableFilterView `getFilteredImage() `
```Swift
let uiImage = filterSwipeView.getFilteredImage()
```


## Next on the list

- [ ] Add support landscape images without quality loss and disorientation
- [ ] Add support more then Two CIFilters in the Combined DSFilter
- [ ] Expan the library with also Drawing on the images



### Please feel free to comment and suggest improvements over PR's. 

