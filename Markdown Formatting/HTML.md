# Directory
<a id="top"></a>
- [Tables](#Tables)
	- [Rowspan](#Rowspan)
	- [Colspan](#Colspan)

## Tables
### Rowspan
<table>
    <thead>
        <tr>
            <th>Layer 1</th>
            <th>Layer 2</th>
            <th>Layer 3</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=4>L1 Name</td>
            <td rowspan=2>L2 Name A</td>
            <td>L3 Name A</td>
        </tr>
        <tr>
            <td>L3 Name B</td>
        </tr>
        <tr>
            <td rowspan=2>L2 Name B</td>
            <td>L3 Name C</td>
        </tr>
        <tr>
            <td>L3 Name D</td>
        </tr>
    </tbody>
</table>

```
<table>
    <thead>
        <tr>
            <th>Layer 1</th>
            <th>Layer 2</th>
            <th>Layer 3</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=4>L1 Name</td>
            <td rowspan=2>L2 Name A</td>
            <td>L3 Name A</td>
        </tr>
        <tr>
            <td>L3 Name B</td>
        </tr>
        <tr>
            <td rowspan=2>L2 Name B</td>
            <td>L3 Name C</td>
        </tr>
        <tr>
            <td>L3 Name D</td>
        </tr>
    </tbody>
</table>
```

### Colspan
<table>
	<thead>
		<tr>
			<th colspan=2><b>customers</b></th>
			<th><b>...next table...</b></th>
			<th colspan=2><b>produce</b></th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><b>id</b></td>
			<td><b>name</b></td>
			<td><b>...next table...</b></td>
			<td><b>id</b></td>
			<td><b>name</b></td>
		</tr>
		<tr>
			<td>101</td>
			<td>Michael</td>
			<td><b>...next table...</b></td>
			<td>1</td>
			<td>Lettuce</td>
		</tr>
		<tr>
			<td>102</td>
			<td>Katrina</td>
			<td><b>...next table...</b></td>
			<td>2</td>
			<td>Tomato</td>
		</tr>
		<tr>
			<td>103</td>
			<td>John</td>
			<td><b>...next table...</b></td>
			<td>3</td>
			<td>Banana</td>
		</tr>
	</tbody>
</table>

```
<table>
	<thead>
		<tr>
			<th colspan=2><b>customers</b></th>
			<th><b>...next table...</b></th>
			<th colspan=2><b>produce</b></th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><b>id</b></td>
			<td><b>name</b></td>
			<td><b>...next table...</b></td>
			<td><b>id</b></td>
			<td><b>name</b></td>
		</tr>
		<tr>
			<td>101</td>
			<td>Michael</td>
			<td><b>...next table...</b></td>
			<td>1</td>
			<td>Lettuce</td>
		</tr>
		<tr>
			<td>102</td>
			<td>Katrina</td>
			<td><b>...next table...</b></td>
			<td>2</td>
			<td>Tomato</td>
		</tr>
		<tr>
			<td>103</td>
			<td>John</td>
			<td><b>...next table...</b></td>
			<td>3</td>
			<td>Banana</td>
		</tr>
	</tbody>
</table>
```
	
## Documents
### Anchors
- `<a href="#top">Top</a>` &mdash; Can be left empty to be invisible
- `<a id="top"></a>` &mdash; Can be left empty to be invisible
	
e.g.: <a href="#top">Top</a>