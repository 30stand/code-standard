# Accessibility

Work in progress

Todo:

1.  xxx
1.  yyy
1.  zzz


### Form control
1. For all input elements of type text, file or password, for all textareas and for all select elements in the Web page, a label element is attached before the input, textarea, or select element. The for attribute of the label element matches the id of the input, textarea, or select element.
	
	Sample code:
	```
	<label for="firstname">First name:</label> 
	<input type="text" name="firstname" id="firstname" />
	```

1. For all input elements of type checkbox or radio in the Web page, the label is positioned after the input element. The for attribute of the label element matches the id of the input element.
	
	Sample code:
	```
	<input type="checkbox" id="markuplang" name="computerskills" checked="checked">
	<label for="markuplang">HTML</label>
	```

1. Group the logically related input or select element within fieldset elements and each fieldset should has a legend element that describes the group. Sample code:

	```
	<form action="http://example.com/adduser" method="post">
	   <fieldset>
	     <legend>Residential Address</legend>
	     <label for="raddress">Address: </label>
	     <input type="text" id="raddress" name="raddress" />
	     <label for="rzip">Postal/Zip Code: </label>
	     <input type="text" id="rzip" name="rzip" />
	     ...more residential address information...
	   </fieldset>
	   <fieldset>
	     <legend>Postal Address</legend>
	     <label for="paddress">Address: </label>
	     <input type="text" id="paddress" name="paddress" />
	     <label for="pzip">Postal/Zip Code: </label>
	     <input type="text" id="pzip" name="pzip" />
	     ...more postal address information...
	   </fieldset>
	</form>
	```
