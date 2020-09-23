<div align="center">

## Multiple Select Combo box


</div>

### Description

Multiple Select combo with form validation for minimum and maximum selections
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Sine45](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/sine45.md)
**Level**          |Intermediate
**User Rating**    |4.8 (19 globes from 4 users)
**Compatibility**  |Java \(JDK 1\.1\), Java \(JDK 1\.2\)
**Category**       |[Internet/ Browsers/ HTML](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/internet-browsers-html__2-68.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/sine45-multiple-select-combo-box__2-3202/archive/master.zip)





### Source Code

```
<HTML>
<HEAD>
<META NAME="Author" Content="Tanwani Anyangwe">
<TITLE>Multiple - Select Box</TITLE>
</HEAD>
<BODY>
<P>&nbsp;</P>
<script>
function MultiCombo(name,value,options){
	this.name = name;
	this.options = options;
	this.value = value;
	this.size = 5;
	this.delimeter = ","
	//this.formName = "document.forms[0]";
	this.formName = document.forms[0];
	this.leftOptions = new Array()
	this.rightOptions = new Array()
	this.caption = name.toUpperCase();
	this.minRequired = 0;
	this.maxRequired = 100;
	this.build = _build;
	this.fillCombos = _fillCombos;
	this.onChange = _onChange;
	this.onClick = _onClick;
	this.onSubmit = _onSubmit;
	this.hiddenField = _hiddenField;
	this.button = _button;
	this.listBox = _listBox;
}
function _onChange(sfrom,sto){
	return "if(this.form.autoSelect"+ this.name +".checked){"+ this.onClick(sfrom,sto,false) +"};"
}
function _onClick(sfrom,sto,ball){
	var s = "var l=this.form."+ sfrom +";var r=this.form."+ sto +";"
	if (ball){
		s += "for(i=0;i<l.length;i++){if(l.options[i].value!='_blank'){r.options[r.length]=new Option(l.options[i].text,l.options[i].value);l.options[i]=null;--i;}};"
	}
	else {
		s += "var i=l.selectedIndex;if(i==-1){alert('Select an item first!');return false;};if(l.options[i].value!='_blank'){r.options[r.length]=new Option(l.options[i].text,l.options[i].value);l.options[i]=null;};"
	}
	s += "for(i=0;i<r.length;i++){if(r.options[i].value=='_blank'){r.options[r.length]=new Option(r.options[i].text,r.options[i].value);r.options[i]=null;}};"
	s += "var s=''; for(i=0;i<this.form."+ this.rightName +".length;i++){if(this.form."+ this.rightName +".options[i].value!='_blank'){s = s + this.form."+ this.rightName +".options[i].value + ',';}};this.form."+ this.name + ".value=s;"
	return s;
}
function _onSubmit(){
	var s = "if(this.right"+ this.name + ".length-1<"+ this.minRequired +"){alert('You must select at least "+ this.minRequired +" "+ this.caption +"');this.left"+ this.name + ".focus();return false;};"
	s = s +"if(this.right"+ this.name + ".length-1>"+ this.maxRequired +"){alert('You must select at most "+ this.maxRequired +" "+ this.caption +"');this.left"+ this.name + ".focus();return false;};"
	return s;
}
function _build(){
	var spacer;
	spacer = "<div style=\"font-size:1pt;\">&nbsp;</div>";
	this.value = this.value.split(this.delimeter)
	this.options = this.options.split(this.delimeter)
	this.leftName = "left" + this.name;
	this.rightName = "right" + this.name;
	this.fillCombos();
	var s = "<table class=\"combo_multiple\" border=\"0\" cellspacing=\"0\" cellpadding=\"2\">"
	s += "<tr><caption><b>"+ this.caption +"</b></caption><th>Available Choices<br>"
	s += this.listBox(this.leftName,this.leftOptions,this.onChange(this.leftName,this.rightName));
	s += "</th><th>"
	s += "<input name=\"autoSelect"+ this.name +"\" title=\"Auto Select\" type=\"checkbox\">";
	s += spacer;
	s += this.button("&gt;&gt;", this.onClick(this.leftName,this.rightName,true));
	s += spacer
	s += this.button("&nbsp;&gt;&nbsp;", this.onClick(this.leftName,this.rightName,false))
	s += spacer
	s += this.button("&nbsp;&lt;&nbsp;", this.onClick(this.rightName,this.leftName,false))
	s += spacer
	s += this.button("&lt;&lt;", this.onClick(this.rightName,this.leftName,true))
	s += "</th><th>Selected Choices<br>"
	s += this.listBox(this.rightName,this.rightOptions,this.onChange(this.rightName,this.leftName))
	s += "</th>"
	s += "</tr></table>";
	s += this.hiddenField();
	this.formName.onsubmit = new Function(this.onSubmit());
	//eval(this.formName).onsubmit = new Function(this.onSubmit());
	document.write (s);
}
function _hiddenField(){
	return "<input type=\"hidden\" name=\""+ this.name +"\" value=\""+ this.value.join(",") +"\">\n";
}
function _listBox(sName,aOptions,sOnChange){
	var s = "<select size=\""+ this.size +"\" name=\""+ sName +"\" onChange=\""+ sOnChange +"\" multiple>\n";
	for(var i=0;i<aOptions.length;i++) {
		s += "<option value=\""+ aOptions[i][0] +"\" >" + aOptions[i][1] + "</option>\n";
	}
	s += "</select>\n";
	return s;
}
function _button(sValue,sOnClick){
	return "<input type=\"button\" name=\"btn"+ this.name + sValue +"\" value=\""+ sValue +"\" onClick=\""+ sOnClick +"\" class=\"btn_combo\">";
}
function _fillCombos(){
	var i,j
 	var text,value;
  	var blank = "";
  	for(i=0;i<30;i++){blank += "&nbsp;"};
  	for(i=0;i<this.options.length;i++){
  		if( this.options[i].indexOf("|") > -1 ){
  			var temp_ar = this.options[i].split("|");
  			value = temp_ar[0];
  			text = temp_ar[1];
  		}
  		else {
  			var value = this.options[i];
  			var text = this.options[i];
  		}
		var found = SearchArray(this.value,value);
		if (!found){
			this.leftOptions[this.leftOptions.length] = new Array()
			this.leftOptions[this.leftOptions.length-1][1] = text;
			this.leftOptions[this.leftOptions.length-1][0] = value;
		}
		else {
			this.rightOptions[this.rightOptions.length] = new Array()
			this.rightOptions[this.rightOptions.length-1][1] = text;
			this.rightOptions[this.rightOptions.length-1][0] = value;
		}
  	}
	this.leftOptions[this.leftOptions.length] = new Array()
	this.leftOptions[this.leftOptions.length-1][1] = blank;
	this.leftOptions[this.leftOptions.length-1][0] = "_blank";
	this.rightOptions[this.rightOptions.length] = new Array()
	this.rightOptions[this.rightOptions.length-1][1] = blank;
	this.rightOptions[this.rightOptions.length-1][0] = "_blank";
}
function SearchArray(Ar,val){
	for(var i=0;i<Ar.length;i++){
		if(Ar[i]==val){return true;}
	}
	return false;
}
</script>
<form onsubmit="" id=form1 name=form1 action="#">
<script>
var allOptions = "1|Mark Twain,2|Tanwani Anyangwe,3|Charles Dickens,4|Micheal Crichton,5|Stephen King,6|Jean Jacques Voltaire";
var myvalues = "1,5,6";
var g = new MultiCombo("authors",myvalues,allOptions);
g.minRequired = 4;
g.maxRequired = 5;
g.build();
</script>
<input type=submit value=send>
</form>
</BODY>
</HTML>
```

