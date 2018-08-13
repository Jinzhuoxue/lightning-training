Day 1 : Lightning Component Basic
1. Lightning Component Framework: What, Why and How
	1. *What* :  Lightning Component framework is a UI framework for developing dynamic web apps for mobile and desktop devices
	2. *Why*  
		* Out-of-the-Box Component Set 
		* Rich component ecosystem
		* Performance
		* Event-driven architecture
		* Faster development
		* Device-aware and cross browser compatibility
	4. *How* 
		 * Browser Support 
		 * My Domain Is Required
		 * Developer Console, Eclipse, VS Code
		 
2. Lightning Component Bundle
	* *component* The only required resource in a bundle. Contains markup for the component.
	* *controller* Contains client-side controller methods to handle events in the component.
	* *helper* JavaScript functions that can be called from any JavaScript code in a component’s bundle
	* *style* Contains styles for the component.
	* *other* renderer, design, svg, document
3. Component IDs
	* *Local IDs* A local ID is an ID that is only scoped to the component: getLocalId()
	* *Global IDs* Every component has a unique globalId, which is the generated runtime-unique ID of the component instance: getGlobalId()
4. Component Attributes : Use the <aura:attribute> tag to add an attribute to the component
	* Attribute Naming Rules: 
		* Must begin with a letter or an underscore. 
		* Must contain only alphanumeric or underscore characters
	* Types
		* Basic Types   =>  Java Basic Types
		* *Function Type*  => JS Function, only be used on the client side
		* *Object Types* => java.lang.Object : ignore any conversion for its attribute
		* Standard and Custom Object Types => SobjectType
		* Collection Types => Java Collection Types
		* Custom Apex Class Types => Custom classes used for component attributes shouldn’t be inner classes or use inheritance
		* Framework-Specific Types =>  Aura.Component, Aura.Component[],  Aura.Action
	* Expressions : An expression is any set of literal values, variables, sub-expressions, or operators that can be resolved to a single value. Method calls are not allowed in expressions. The expression syntax is: {! expression }
		* Data Binding Between Components: *{! expression}*(Bound Expressions) and *{# expression}* (Unbound Expressions)
		* Value Providers ： v - component’s attribute set *{! v.attr }*and c-component’s controller *{! c.actionHandler }*
		* Global Value Providers : globalID, $Browser, $Label, $Locale, $Resource
		* [Expression Operators Reference](https://developer.salesforce.com/docs/atlas.en-us.lightning.meta/lightning/expr_operators.htm)  [Expression Functions Reference](https://developer.salesforce.com/docs/atlas.en-us.lightning.meta/lightning/expr_functions.htm)
	* Accessing Component Attributes: cmp.get(“v.attributeName“) ; cmp.set(“v.attributeName“, “attribute value”)
5. Communicating with Events
	* Actions and Events (Browser Events) 
		* <lightning:button label = “Click Me” onclick = “{!c.handleClick}” />
		[image:B3C516BA-3226-4FF0-80A6-204349A3CCD1-807-0001BB134CD5C9DB/214.0.png]
		
	* Component Events : A component event is fired from an instance of a component. A component event can be handled by the component that fired the event or by a component in the containment hierarchy that receives the event.
		* The sequence of component event propagation. *Event fired* => *Capture phase* => *Bubble phase*
		* Create Custom Component Events : <aura:event type=“COMPONENT”>  attribute definition </aura:event>
		* Fire Component Events : <aura:registerEvent name=“componentEventName” type=“c:compEvent”/> 
```
		const compEvent = cmp.getEvent("sampleComponentEvent");
		compEvent.fire();
```
		* Handling Component Events
```
<aura:handler name="sampleComponentEvent" event="c:compEvent"
action="{!c.handleComponentEvent}"/>	
```

	*  Application Events : Application events follow a traditional publish-subscribe model. An application event is fired from an instance of a component. All components that provide a handler for the event are notified.
	* Event Handling Lifecycle
[image:1A2924D8-C492-4955-848D-FD8E2B8426FF-807-0001BEB3BB88EDDE/214.0.png]
6. Assignment
Create a general picklist component,  using SobjectType Name and Field API Name as public attribute and register a component event named ‘onchange’.