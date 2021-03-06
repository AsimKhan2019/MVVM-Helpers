# Julmar Model-View-ViewModel and Core .NET library
**Copyright (C) 2008-2017 julmar.com**

This library is provided "as-is" with no warranty. It was developed by JulMar Technology, Inc. and is  
distributed from www.julmar.com. You are free to utilize the source code (in whole, or in part) or 
provided assembly however you desire, including creating derivative works without any compensation or requirements back to JulMar Technology, Inc. This library was intended to be used as a learning and teaching aid, and I hope it has some value to each person who looks at it.

# Versions

There are three versions of the library available:

**Cross-Platform Edition**
This supports .NET 4.5, Mono 4.5, Windows Store, Windows Phone (WinPRT), Xamarin.iOS and Xamarin.Android with a Portable Class Library and a set of platform-specific framework DLLs. This is the preferred release as it automatically detects your platform and installs the right things with Nuget.  **Install the MVVMHelpers.PCL version for this**

**WPF (3.5, 4.0 and 4.5)**
This version is the older and more complete version which includes a variety of classes for .NET in general as well as MVVM, Behaviors and UI services for WPF.

**Windows Store Apps (8.0, 8.1)**
This version is newer and is a derivative of the original WPF version.  It includes base MVVM support and a port of the Blend behavior system (since that was unavailable at the time).

# Release Notes
## WPF
**1.0** 
Initial revision - all basic functionality is present.

**1.01: rolled in a bunch of fixes from internal library -- 6/09**
Fixed a bug in the event commander which was causing multiple invocations in some cases.
Added support for ShowDialog return results.
Added HelpProvider behavior to support invoking Windows Help
Removed automatic mediator registration from ViewModel - unnecessary perf hit when not using service mediator - you must call RegisterWithMessageMediator() deliberately now.
Added SystemInfo class to retrieve Windows version - can detect difference between W2K8 SP2 and Windows 7 (Environment.OSVersion does not appear to do so).
Added LinearGradientMarkupExtension for easy gradients
Added ENTER/ESC/Fx/CTRL support to NumericTextBoxBehavior.
Added DelegatingCommand<T>
Added ObservableDictionary<K,V>

**1.02: additional support 7/09**
Added ScrollingPreviewService
Added CommandParameter and Command to EventCommander event arguments
Added Past/Drop conversion to NumericTextBoxBehavior
Split out EditingViewModel into implementation class to make it easier to provide other forms of edit support.
Added PropertyObserver<T> from Josh Smith

**1.03: Added new Behaviors assembly  7/30**
Added dependency to System.Windows.Interactivity.dll
Ported over existing attached behaviors to Blend style behaviors [BREAKING CHANGE](BREAKING-CHANGE)
Added WatermarkedTextBoxBehavior
Added InvokeCommand action to bind to VM ICommands
Added CommandEventTrigger to support EventCommander from Blend

**1.04: 9/15**
Added Designer.InDesignMode static property to test design surface
Added test for null conditions in VisualTreeHelper extensions
Moved ValidatingViewModel into proper namespace
Added clipboard paste support to the WatermarkedTextBoxBehavior
Changed MTObservableCollection<T> to support true multi-threaded access based on discussion on WPFDisciples list.

**1.05 11/1**
Added support for VS2010 Beta 2
Removed ViewModel.OnPropertiesChanged - merged into ViewModel.OnPropertyChanged [BREAKING CHANGE](BREAKING-CHANGE)
Added generic support to MessageMediator
Added BindingTrigger to trigger of ViewModel binding values in Blend
Added CloseWindowBehavior to auto-close a dialog or modaless form without code behind
Added SelectTextOnFocusBehavior to select all text in a TextBox when it receives focus
Added ViewportSynchronizerBehavior to track the ViewPort of a ScrollViewer and bind it to ViewModel properties.
Added Dispatcher transition for RaiseClose and RaiseActivate from VM for cross-thread invocation
Added MultiConverter to aggregate value converters together.
Added ScrollingPreviewBehavior and ScrollBarPreviewBehaviors (replaced ScrollingPreviewService)
Added DeferredScrollBehavior

**1.06 4/2010**
Added new behaviors and converters.  Synched with private library

**2.00 4/2010**
First full targeted .NET 4.0 release
Added MEF support to locate services using [ExportServiceProvider](ExportServiceProvider)
Added MEF support to locate ViewModels using [ExportViewModel](ExportViewModel)
Added MEF support to locate Views using [ExportUIVisualization](ExportUIVisualization)
Cleanup of library to target both .NET 3.5 and .NET 4.0

**3.00 6/2010**
Added undo/redo framework
Added CollectionObserver
Updated PropertyObserver to allow global property notifications
Added DataGridRowDragBehavior
Added ItemsControl drag/drop behavior

**3.5 7/2010**
Split out Julmar.Core to contain non-WPF specific types.
Moved internal ThreadedCollection into Core
Added ReaderWriterLockSlim extensions and ObjectLock extensions
Added DataGridRowIndexBehavior

**4.00 8/2010**
Added ObjectCloner
Added SelectedItemsCollectionSynchronizer

**4.01 12/2010**
Official build from rcat.codeplex.com changes
Added attached event support to EventCommander
Corrected issue with MessageMediator identifying interface targets from an implementation message
Added new constructor to ViewModel to avoid MEF registration for 3.5 memory leak issue (MEF)
Added Swap and Move extensions to IList collections

**4.02 1/2011**
Added option to defer collection change UNDO records into a group for global undo.  BeginDefer/EndDefer on CollectionUndoObserver.

**4.03 2/2011**
Added flag to turn off CommandManager.RequerySuggested if VM wants to handle it directly.
Added lambda version of OnNotifyPropertyChanged per request
Unit tests for above.

**4.04 3/2011**
Changed MEF resolution code to allow custom catalogs to be used for resolving dependencies.
Added Range class for Parallel programming
Added ListView sorting behavior
Added 2 overrides for IUIVisualizer.Show and ShowDialog to pass object owner for explicit window ownership management (to be used by view, not VM).

**4.05 4/2011**
Added ExceptionExtensions
Added InDesigner property to ViewModel (just a copy of Designer.InDesignerMode)
Added MaskedTextBoxBehavior
Added new overrides for IMessageVisualizer to support icons, window owner, etc.

**4.06 8/2011**
Allow ExportUIVisualizer to be applied more than once.
Remove IViewModelTrigger and rewrote ViewModelTrigger behavior to target event by name.
Added MultiTreeSelect behavior
Modified MTObservableCollection to support suspension of events
Added ChangeCursorAction to behaviors

**4.07 12/2011**
Fixed ExportUIVisualizer (removed AllowMultiple as it broke certain resolutions with MEF).
Added StyleInteraction and test project into behaviors project
Added SelectTextAction, MessageBoxAction and AutoDisabledImageBehavior
Fixed a couple of spelling errors in comments.

**4.08 2/2012**
Enabled DeferredBinder to support 2-way bindings
Added test project for DeferredBinder
Added back in support for multiple ExportUIVisualizer and ExportViewModel attributes
Added test project for multiple export attributes
Removed IDynamicResolver interface, renamed MefComposer to DynamicComposer.  You should just use DynamicComposer.Instance as the library is too dependent on MEF to really change the composition model.
Added ListViewColumnAutoSizeBehavior to provide Grid-like column sizing (Auto,*,##)
Added test project for ListViewColumnAutoSizeBehavior
Modified ListViewSortBehavior to correct crash when adorner layer is not present.
Fixed bug in ValidationManager when traversing properties and potentially getting into infinite loop
Added MouseGestureScrollViewerBehavior to support iPad-like gestures with mouse on ScrollViewer elements (with inertia)

**4.09 3/2012**
Added check in SynchronizedScrollingBehavior to disable scrolling if scrollbar is disabled.
Added ability to turn off drag adorner for ItemsControlDragDropBehavior
Added ServiceReplacement test project + unit tests from blog
Fixes for EditingViewModel, also extended with more interception hooks.

**4.10 6/15/2012**
Refactored some of the services to be more inline with the internal metro/Win8 version.
Merged .NET 3.5/4.0 set together

**4.20 9/2012 (matches 1.04 of MvvmHelpers/Metro)**
Several changes based on work done with MVVMHelpers/Metro.
Removed [ExportService](ExportService), just use [Export](Export) and ServiceLocator will find it.
Renamed ServiceProvider to ServiceLocator.
Renamed IServiceProviderEx to IServiceLocator
Removed ViewModel.ServiceProvider - replaced with ServiceLocator.Instance
ServiceLocator is now exported only as IServiceLocator, not IServiceProvider[Ex](Ex)
Removed EventCommander - use EventTrigger from Blend
Removed LifetimeEvents - use EventTrigger from Blend
MessageVisualizerOptions is now in JulMar.Windows.UI namespace (was in interfaces)
Changed InvokeCommand to pass parameter from trigger if no CommandParameter is data bound
BREAKING CHANGE: Services are no longer marked with [InheritedExport](InheritedExport), you must [Export](Export) any services you want to override.  This was done specifically so that you could implement service interfaces without replacing the built-in ones.
Added Windows 8/2012 constants to SystemInfo
Updated ViewModelTrigger to support Action and Action<T> delegates
ViewModelLocator is not public anymore - use IViewModelLocator
New ViewModelLocatorResource can be placed into resources to find VMs if you don't like ViewModelCreator
Added ServiceLocatorResource (from Win8/Metro)

**4.21 6/2013**
Bug fix for DoubleClickTrigger
Changed version to .NET 4.5

**4.22 8/2013**
Bug fix to allow "#" in path when loading julmar.wpf.helpers.dll
Updated .NET 3.5, 4.0 and 4.5 versions of library.

## Windows Store Apps (Metro)
**1.00**
Initial revision - all basic functionality is present.
Based on Windows 8 CP

**1.01**
Rebuilt for Windows 8 RTM
Ported ViewModelLocator and most of MVVMHelpers 4.10
Ported Blend behavior support

**1.02**
Added NameScopeBinding to allow ElementName binding to attached collection items
Changed InvokeAction to pass trigger parameter if CommandParameter is null.

**1.03**
Fixed a bug in the ViewModelLocator when back-navigation occurs
Removed the public ViewModelLocator breaking change. Use IViewModelLocator interface instead
Added ViewModelLocatorResource for binding in XAML
Added ServiceLocatorResource for binding services in XAML
Added unit tests and new test program

**1.04 9/2012**
Modified ViewModelTrigger to support Action and Action<T>
Added static Designer class to port WPF code
IViewModelLocator moved to JulMar.Windows.Interfaces (instead of Core)
Added InDesignMode property to SimpleViewModel
Removed dead code from ViewModelLocator
Fixed MessageMediator to properly return true/false when targets have been collected
Changed MessageMediator back to public type so it can be used multiple times
Changed ServiceProvider implementation class from public to internal.
Moved MessageVisualizerOptions to JulMar.Windows.UI (was in interfaces)
Updated some unit tests

**1.05 3/2013**
Minor bug fixes
Added Flyout control and IFlyoutVisualizer
Integrated StateManager into PageNavigator and abstracted with IStateManager
Added support to locate ViewModels through attached property (still supports dictionary)
Added support to provide custom serialization on a ViewModel by implementing IViewModelStateManagement

**1.06 3/2013**
Fixes for PageNavigator/StateManager
Expose KnownTypes on IStateManager
Allow persistence even when objects do not participate in INavigateAware
Refactored code to share persistence on suspend + navigation.

**1.07 3/2013**
Fixes to reattach event handlers from EventTrigger when UIElement is unloaded/loaded multiple times.

**1.08 5/2013**
Added SynchronizedCollectionBehavior (ported from WPF version)
Added new AutoSerializingPageNavigator
Added support to replace [Imports](Imports) using ServiceLocator

**1.09 5/2013**
Fixed bug in PageNavigator.NavigateTo(Type,object) not passing along argument.
Fixed bug in VisualStateUtilities.ShouldContinueTreeWalk - missing test.
Renamed FocusManager to FocusScope to avoid namespace collision with WinRT Xaml type
Added WatermarkTextBehavior

**1.10 6/2013**
Added IsWatermarkTextVisible property to WatermarkTextBoxBehavior.
