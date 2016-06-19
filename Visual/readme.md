#Visual

This document contains a high level overview of the most basic custom visual implementation with links to documents that contain more detailed information about each component.

The basic structure of a visual is a class that implements `IVisual` wrapped in a module that is namespaced to allow access to the APIs interfaces. The API version utilized by your visual depends on the version of the d.ts file referenced in your project. 

##Module

To ensure access to all of the correct api interfaces your visual most be created in the `powerbi.extensiblity.visual` namespace.

```typescript
module powerbi.extensiblity.visual {
    //create your visual (class) here
}
```

##Visual class / IVisual

All visuals start with a class that implements the `IVisual` interface. You can name the class whatever you'd like, but there must be *exactly one* class that implements the `IVisual` interface.

**Note:** your visual class name must match what is defined in your `pbiviz.json` file.

```typescript
@VisualPlugin({
    //declare properties of the visual plugin here (used by host)
    capabilities: { ... },
})
class MyVisual implements IVisual {
    
    constructor(options: VisualConstructorOptions) {
        //one time setup code goes here (called once)
    }
    
    public update(options: VisualUpdateOptions): void {
        //code to update your visual goes here (called on all view or data changes)
    }

    public enumerateObjectInstances(options: EnumerateVisualObjectInstancesOptions): VisualObjectInstanceEnumeration {
        //returns objects to populate the property pane (called for each object defined in capabilities)
    }
    
    public destroy(): void {
        //one time cleanup code goes here (called once)
    }
}
```

###@VisualPlugin

The `@VisualPlugin` decorator is used to provide information about your visual to the host. 

* **capabilities** - defines information about the capabilities of your visual including what data is expected, how it should be mapped, properties pane objects, etc... [Learn more about capabilities](Capabilities/readme.md)


###Constructor

`constructor(options: VisualConstructorOptions)`

The constructor of the visual class is called when the visual is instantiated. It can be used for any set up operations needed for your visual.

**VisualConstructorOptions**

* `element: HTMLElement` - a reference to the DOM element that will contain your visual.
* `host: IVisualHost` - a collection of properties and services that can be used to interact with the visual host (Power BI). [Learn more about IVisualHost](IVisualHost.md) 

###update

`public update(options: VisualUpdateOptions): void`

All visuals must implement a public update method. It is called whenever there is a change in the data or host environment.

**VisualUpdateOptions**

* `viewport: IViewport` - the dimensions of the viewport that the visual should be rendered within
* `dataViews: DataView[]` - the dataview object (contains all data needed to render your visual)  
* `type: VisualUpdateType` - flags that indicate the type(s) of this update (Data | Resize | ViewMode | Style | ResizeEnd)
* `viewMode: ViewMode` - the view mode of the visual (view or edit)

###enumerateObjectInstances `optional`

`enumerateObjectInstances(options: EnumerateVisualObjectInstancesOptions): VisualObjectInstanceEnumeration`

This method is called for every object listed in capabilities. Using the options (currently just the name) you return a `VisualObjectInstanceEnumeration` with information about how to display this property.

**EnumerateVisualObjectInstancesOptions**

* `objectName: string` - the name of the object

###destroy `optional`

`public destroy(): void`

The destroy function is called when your visual is unloaded and can be used to do clean up tasks such as removing event listeners.
