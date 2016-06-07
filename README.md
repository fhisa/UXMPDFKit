![UXM Token Field](https://uxmstudio.com/public/images/uxmpdfkit.png)

[![Version](https://img.shields.io/cocoapods/v/UXMPDFKit.svg?style=flat)](http://cocoapods.org/pods/UXMPDFKit)
[![License](https://img.shields.io/cocoapods/l/UXMPDFKit.svg?style=flat)](http://cocoapods.org/pods/UXMPDFKit)
[![Platform](https://img.shields.io/cocoapods/p/UXMPDFKit.svg?style=flat)](http://cocoapods.org/pods/UXMPDFKit)

## Requirements
- iOS 8 or above
- Xcode 7 or above
- Swift 2.1

## Note

This project is still in early stages. Right now the PDF reader works both programmatically and through interface builder. This PDF reader supports interactive forms and provides methods for overlaying text, signature and checkbox elements onto the page, as well as rendering a PDF with the elements burned back onto the PDF. See the example project for how to implement.

## Installation

UXMPDFKit is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod "UXMPDFKit"
```
## Usage
### Simple Usage
UXMPDFKit comes with a single page PDF reader with many features implemented right out of the box. Simply create a new PDFViewController, pass it a document and display it like any other view controller. It includes support for forms, a page scrubber and page scrolling.
```swift
let url = NSBundle.mainBundle().pathForResource("sample", ofType: "pdf")!
let document = PDFDocument(filePath: url, password: "password_if_needed")
let pdf = PDFViewController(document: document)

self.navigationController?.pushViewController(pdf, animated: true)
```


### Single Page Collection View
This collection view renders a PDF in its entirety one page at a time in photo-slideshow style. 
```swift
let collectionView = PDFSinglePageViewer(frame: self.view.bounds, document: self.document)
collectionView.singlePageDelegate = self
```

Its delegate methods are implemented as follows:

```swift
func singlePageViewer(collectionView: PDFSinglePageViewer, didDisplayPage page:Int)
func singlePageViewer(collectionView: PDFSinglePageViewer, loadedContent content:PDFPageContentView)
```


### Forms
User-interactable forms are supported by UXMPDFKit, but only partially. Currently only PDF's versions 1.6 & 1.7 render correctly.

Form features implemented:
* Signatures
* Text fields
* Checkboxes

Form features not yet implemented:
* Radio buttons
* Choice boxes

Form parsing and handling is taken care of by the PDFFormViewController. It takes a document, and then is passed a PDFPageContentView to render form elements onto.
```swift
let formController = PDFFormViewController(document: self.document)
formController.showForm(contentView)
```

PDF rewriting is not currently supported, but flattening inputed data onto the PDF is. To render the form information onto the document, call:
```swift
func renderFormOntoPDF() -> NSURL // Returns a temporary url
func save(url: NSURL) -> Bool // Writes 
```


### Annotations
Coming soon



# Author
Chris Anderson:
- chris@uxmstudio.com
- [Home Page](http://uxmstudio.com)

# License

UXMPDFKit is available under the MIT license. See the LICENSE file for more info.

