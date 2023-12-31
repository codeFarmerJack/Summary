# 1. Tuple, List, Dict and Set
## 	Definition
    In Python, **()**, **[]**, and **{}** are used to denote different types of data structures. 
    Here's a brief explanation of each:
###  	(1) Parenthese () - **Tuple** or Grouping
        * Tuples are ordered, immutable sequence of elements
        * Used for grouping or organizing data. 
        * my_tuple = (1, 2, 3)
### 	(2) Square Brackets [] - **List**:
        * Lists are ordered, mutable sequences of elements
        * Used for storing collections of items
        * my_list = [1, 2, 3]
### 	(3) Curly Braces {} - **Dict** or **Set**
        * Dictionaries: unordered collection of key-value pairs
        * my_dict = {'key1': 'value1', 'key2':'value2'}
        * Sets: unordered collection of unique elements
        * my_set = {1, 2, 3}
## 	Access Element
  	Accessing data in Python depends on the type of data structure you're working with. Here are 
  	some examples for accessing data in tuple, list, dict, and set:
### 	(1) **Tuple**
	my_tuple = (1, 2, 3, 'a', 'b')
	# Accessing elements by index
	first_element = my_tuple[0]
	third_element = my_tuple[2]
### 	(2) **List**
	my_list = [1, 2, 3, 'a', 'b']
	# Accessing elements by index
	first_element = my_list[0]
	third_element = my_list[2]
### 	(3) **Dictionary**
	my_dict = {'name':'John', 'age':25, 'city':'New York'}
	# Accessing values by key
	name_value = my_dict['name']
	age_value = my_dict['age']	
### 	(4) **Set**
	my_set = {1, 2, 3, 'a', 'b'}
	# Sets are unordered, so there's no index to access elements directly 
 	# Checking membership
	element_existence = 'a' in my_set
	
	Keep in mind that for sets, there is no concept of indexing as they are unordered collections 
 	of unique elements. Instead, you typically use methods like **in** to check for membership.

# 2. What is 'plt.gcf()'?
  	'gcf' stands for "get current figure". It is a function that returns a reference to the current 
	figure in the current state of the plot. The figure is the top-level container for all the plot elements. 
  	It is used to obtain a reference to the current figure, and then you can perform operations or 
	modifications on that figure.
## 2.1 plt.gcf().get_axes()
	In matplotlib, the 'get_axes()' method is a function provided by a Figure object. It returns a list of 
 	all the Axes objects contained within that figure. Each Axes object represents a subplot or individual
  	plot in the figure.
   	Here's a brief explanation:
		* Figure: It's the top-level container for all elements of a plot. It can contain multiple subplots
  		(Axes), text elements, and more.
		* Axes: It's the area where the data is plotted. A figure can have one or more axes.
  	The 'get_axes()' method allows you to retrieve a list of all the Axes objects in a figure, which you can
   	then iterate over or manipulate individually.
	
# 3. Determine the common date range
## 	3.1 The DataTimeIndex of two DataFrames partially matches exactly.
    common_date_range = pd.to_datetime(np.intersect1d(optimizedGopro["date_01"], optimizedRT["date_01"]))

    It seems you are using the Python with the pandas library to create a common date range from two 
	DataFrames, optimizedGopro and optimizedRT. The pd.to_datetime function is being used to convert 
 	the result of np.intersect1d (which finds the common elements between two arrays) into a pandas DateTimeIndex.
    Here's a breakdown of what each part of the code does:
		* np.intersect1d(optimizedGopro['date_01'], optimizedRT['date_01']): 
        This finds the common elements (intersection) between the 'date_01' columns of the two DataFrames 
		optimizedGopro and optimizedRT.
		* pd.to_datetime(...) 
        This converts the result of the intersection to a pandas DateTimeIndex. This step is useful if the 
		common elements are not already in a datetime format.

    So, after running this line of code, common_date_range should contain a DateTimeIndex representing the 
	common dates between the 'date_01' columns of optimizedGopro and optimizedRT.

## 	3.2 There's a time overlap between two DataFrames
### 3.2.1 pd.merge(...)
		If you want to retrieve the data corresponding to the overlapping time index between two DataFrames, you can
		use the merge operaton in Pandas. Here's an example of how you might implement this:
		# Merge DataFrames based on the 'date_01' column
		merged_data = pd.merge(optimizedGopro, optimizedRT, on='date_01', how='inner', suffixes=('_gopro', 'rt'))
			* on = 'date_01': Specifies that the merge operation should be performed based on the 'date_01' column.
			* how = 'inner': Performs an inner join, keeping only the rows where there's a match in both DataFrames.
			This ensures that you retain only the overlapping time indices.
			* suffixes = ('_gopro', '_rt'): If there are columns with the same name in both DataFrames, this parameter
			adds suffix to the column names to differenciat them.
### 3.2.2 pd.merge_asof(...)
		# Make sure the time columns are in datetime format
		df1['time'] = pd.to_datetime(df1['time'])
		df2['time'] = pd.to_datetime(df2['time'])
		
		# Merge two dataframes based on the nearest time index
		merged_data = pd.merge_asof(df1, df2, on = 'time', direction = 'nearest')
			* on = 'time': Specifies the column used for merging, which is the time column
			* direction = 'nearest': Specifies to merge with the nearest key rathet than requiring an exact match.
### 3.2.3 Comparison of merge() and merge_asof()
####	merge()
		* Use Case: Suitable for mergin on exact matches of the specified key(s)
		* matching: Performing exact matching based on the specified key(s)
####	merge_asof()
		* Use Case: Suitable for merging on approximate matches, particularly useful for time-series data where
		you want to merge based on the nearest key.
		* Matching: Performs approximate matching based on the specified key(s) and includes the nearest keyvalues.

# 4. fig, ax = plt.subplots() 
    It is a common way to create a Matplotlib figure ( '**fig**') and a set of axes ('**ax**') in a single line. 
	This method is convenient and returns a tuple containing both the figure and axes objects.
        * fig: This variable holds the entire figure. It represents the entire window or page where your plots are drawn.
        * axes: This is a collection of all the individual subplots (or axes) within the figure . It is usually a 2D array, 
		so you can access each subplot using index (e.g., 'axes[0, 0] for the top-left subplot)

# 5. **zip**
    zip "pairs" up the elements of a number of lists, tuples, or other sequences, to create an iterator of tuples. 
	The zip function is used to combine elements from multiple iterables into tuples. Here's the basic syntax 
 	of the zip function:
    
    zip(iterable1, iterable2, ...)
	    * iterable1, iterable2, etc.: These are the iterables (lists, tuples, etc.) whose elements you want 
	 	to zip together
	    * The zip function returns an iterator of tuples where the i-th tuple contains the i-th element from 
	 	each of the argument sequences. It stops when the shortest input iterable is exhausted.

# 6. function of comma (,) and set_xdata
    import matplotlib.pyplot as plt
    # Some sample data
    x_data = [1, 2, 3, 4, 5]
    y_data = [2, 4, 6, 8, 10]
    # Without comma (no unpacking)
    line_no_comma = plt.plot(x_data, y_data, label='Original Line no comma')
    # With comma (unpacking)
    line_with_comma, = plt.plot(x_data, y_data, label='Original Line with comma')

    # Create a simple line plot
    new_x_data = [0, 1, 2, 3, 4]
    line_with_comma.set_xdata(new_x_data)

	* If you omit the comma when unpacking the result of plt.plot, the variable on the left side of the 
	assignment will be assigned the entire list of Line2D objects, not just the first element. 
	The comma is crucial for unpacking a single element from the list returned by plt.plot.
	* set_xdata allows you to update the x-coordinates of the points in a line plot. 
    
    In this example, set_xdata is used to update the x-data of the line plot. After calling this method, the 
	line will be redrawn with the new x-coordinates.

# 7. for i, y_value in enumerate(y_data):
    In this example, enumerate(y_data) generates pairs of (index, y_value) as you iterate over y_data, allowing 
	you to access both the index ('i') and the corresponding 'y' value.

# 8. common_data = data[df[date_column].isin(common_date_range)]
## 	(1) df[date_column]: 
	This extracts the values in the 'date_column' column of the DataFrame df.
## 	(2) .isin(common_date_range): 
	This is a method of pandas Series that checks whether each value in the Series is contained in the 
	'common_date_range', which is a precomputed intersection of date ranges between optimizedGopro and optimizedRT.
        * The isin(common_date_range) function returns a boolen mask, indicating whether each element in the 
		Series(in this case, the 'date_column' Series of the DataFrame) is contained in the specified 'common_date_range'.
        * The resulting boolean mask has the same length as the original Series.
        * If an element in the 'date_column' is in 'common_date_range', the corresponding position in the 
		boolean mask will be True.
        * If an element is not in 'common_date_range', the corresponding position in the boolean mask will be False.
        * A boolean mask in the context of pandas refers to a Series or DataFrame of boolean values that has the same 
		length as the original data. The purpose of a boolean mask is to identify which elements in the data satisfy 
  		a certain condition.
## 	(3) This boolean mask is then used to filter the 'data' column, 
		ensuring that only the rows corrsponding to the overlapping time period are included in the visualization.
        * Filtering data by a boolean mask in pandas is straightforward. Once you have a boolean mask, you can use 
		it to index into your DataFrame to retrieve only the rows where the mask is True.

# 9. enumerate()
    for i, (df, date_column, data, label, filtered_data) in enumerate(subplot_layout, start=1):
    plt.subplot(4, 2, i)

    The related syntax for the enumerate function in Python is as follows:
    'enumerate(iterable, start = 0)'
    The enumerate() function is commonly used to iterate over a sequence while keeping track of the index(position) of 
	the current item. The start index(position) can be set via **start**.
        * iterable: This is the sequence, collection, or iterator you want to iterate over.
        * start: This is an optional parameter, and its default value is 0. It represents the starting value of the 
		counter. (i.e., i = 1, in the code snippet above)

# 10. f-string
    An f-string, short for formatted string literal, is a way to embed expressions inside string literals, using a 
	concise and readable syntax.

    Syntax as follows:
    label = f'{filtered_data}Opt' 
        * f'...': This denotes an f-string. The 'f' character before the opening quote indicates that this string is 
		a formatted string literal, allowing you to embed expressions inside curly braces{}
        * {filtered_data}: This is a placeholder for the value of the variable filtered_data. The expression inside 
		the curly braces will be replaced with the actual value of the variable when the string is created.
        * 'Opt': This is a regular string that is appended to the value of the filtered_data variable.

# 11. r prefix
    The r prefix before a string indicates a raw string literal. When you use the r prefix, backslashes (\) in the 
	string are treated as literal characters rather than as escape characters.

# 12. axvline() explanation.
	axvline(...) is a function in Matplotlib that is used to add a vertical line to a plot. It's syntax is as follows:
 	'ax.axvline(x, ymin = 0, ymax = 1, **kwargs)'
  		* x: the x-coordinate at which the vertical line will be drawn
		* ymin (optional): The lower y-coordinate of the vertical line. The default is 0, which corresponds to the 
  		bottom of the plot
		* ymax (optional): The upper y-coordinate of the vertical line. The dafult is 1, which corresponds to the 
  		top of the plot.
		* **kwargs: Additional keyword arguments that control the appearance of the line, such as color, linestyle, 
  		linewidth, etc.

# 13. 'global' keyword
	The 'global' keyword is used to indicate that a variable is a global variable, meaning that it should be accessed 
 	or modified at the global scope rather than the local scope of a function or block.
  	When you declare a variable as 'global', it means that the variable belongs to the global scope (i.e., it is defined
   	outside any function or block) and can be accessed and modified from anywhere in the program.
	It's worth noting that the use of global variables should be done with caution, as it can make the code more difficult
 	to understand and maintain. It's generally recommended to minimize the use of global variables and, when possible, pass
  	variables as parameters to functions.

# 14. plt.gcf().canvas.mpl_connect('button_press_event', on_plot_click) explanation
	This line of code is using the Matplotlib library to connect a callback function ('on_the_plot') to the 
	'button_press_event' event on the canvas of the current figure ('plt.gcf()')
  		* plt.gcf(): This is a matplotlib function that stands for "get current figure". It returns a reference 
		to the current figure in your matplotlib plot.
  		* canvas: The canvas is the drawing area of the figure, where the actual plotting takes place. 
		'plt.gcf().canvas' gives you access to the canvas associated with the current figure.
  		* mpl_connect('button_press_event', on_the_click): This is a method of the matplotlib canvas that is used 
		to connect a callback function to a specific event. In this case, it's connecting the 'on_plot_click' 
		function to the 'button_press_event' event.
			- 'button_press_event': This is the type of the event you want to connect to. In this case, it's the 
			event that is triggered when a mouse button is pressed.
	  		- 'on_plot_click': This is the callback function that will be executed when the specified event occurs. 
			It's a function that you define elsewhere in your code.
	When a button press event occurs on the plot, matplotlib will call the 'on_the_click' function, passing information 
	about the event as an argument to that function. This allows you to respond to user intractions with the plot.

# 15. callback function
	A callback function, also known simply as a callback, is a function that is passed as an argument to another function 
	or method. The purpose of a callback is to be executed at a later time or in response to a specific event. 

# 16. press_button_event
	The 'press_button_event' is a specific type of event in matplotlib that is triggered when a mouse button is 
	pressed. It's part of matplotlib's event handling system, which allows you to interact with a plot.
  	Matplotlib defines a set of standard events that you can connect to, and 'button_press_event' is one of them. 
	Other events include 'button_release_event', 'motion_notify_event', and more. Each event corresponds to a 
	specific user action or interaction with the plot.
 	When you use 'mpl_connect' to connect a callback function to an event, you specify the event type as the 
	first argument.

# 17. existing_lines = [line for line in ax.lines if 'cursor' in line.get_label()]
	The line of code is using a list comprehension to create a list called 'existing_lines'
		* ax.lines: This is a collection of lines in a matplotlib axes ('ax'). Each line typically corresponds 
		to a plot or a graphical element on the axes.
		* 'line.get_label()': This method is used to retrieve the label associated with a line. Labels are often 
		used for items in the legend or for identification.
		* 'for line in ax.lines': This part of code iterates over each line in the collection of lines
  		* 'if 'cursor' in line.get_label()': this condition checks whether the string 'cursor' is part 
		of the label associated with the current line.
		* 'existing_lines': This list comprehension creates a new list ('existing_lines') containing only 
		the lines for which the condition ''cursor' in line.get_label()' is True.
	After running this line of code, 'existing_lines' will contain all the lines the axes 'ax' that have a label 
	containing the string 'cursor'. This can be useful, for example, if you want to remove or modify those lines 
	before adding a new one.

# 18. list comprehension
	List comprehension is a concise and expressive way to create lists in Python. It provides a more readable 
	and often more compact syntax for generating lists compared to using a traditional 'for' loop. List 
	comprehensions are a Pyhonic way to express the creation of lists based on existing iterables or other 
	sequences. The basic syntax of a list comprehension is:
	[expression for item in iterable if condition]
 		* expression: the value you want to include in the new list
   		* item: Variable representing each element in the iterable
	 	* iterable: The original iterable (e.g., list, tuple, string) that you are iterating over
   		* if condition (optional): An optional condition that filters the items. Only items satisfying the 
		condition are included in the new list.

# 19. plt.gcf().get_axes()
		* 'plt': This likely refers to an instance of a plot or chart, usually created with a library like 
		matplotlib.
  		* 'gcf()': Stands for "get current figure." This retrieves the current figure, which is essentially 
		the window or canvas where your plot is being displayed.
  		* 'get_axes()': This method retrieves a list of all the Axes objects in the current figure.
	So, this line of code gives you a list of all the axes (subplots) in the current matplotlib figure.
 	Each Axes object represents an individual plot or subplot.

# 20. figure, subplot, canvas, and axes in matplotlib
	(1) Figure(fig):
 		* The figure is the top-level container for all elements of the plt.
   		* It is the overall canvas, representing the entire area where visual elements are drawn.
	 	* When you create a plot in matplotlib, you typically start by creating a figure using plt.figure() 
		or plt.subplot().
	(2) Canvas:
 		* The canvas is the area of the figure where the visual representation of your plot is actually rendered.
   		* It is the surface upon which the axes(subplots) and other graphical elements are drawn.
	(3) Subplot:
  		* A subplot is a specific region within the canvas where an individual plot or set of plots is displayed.
		* Multiple subplots can be arranged in rows and columns within a single figure.
  	(4) Axes:
   		* An axes is the individual plotting area within a subplot or directly within the figure.
	 	* It includes the coordinate system, ticks, labels, and any other graphical elements associated with a 
		specific plot.
	So, in a nutshell:
 		A figure is the top-level container representing the entire canvas. The canvas is area within the figure 
		where all visual elements are rendered. A subplot is a specific region within the canvas where plots are 
		displayed, and multiple subplots can be arranged in a grid. An axes is an individual plotting area within 
		a subplot or directly within the figure.

# 21. y_value_data = df[data][df[date_column] == initial_x_value].values[0]
	This line of code is used to retrieve a specific value from the DataFrame df
	Here's the breaddown:
		* df: This is the Pandas DataFrame from which you want to extract specific value
		* data: This is a variable containing the column name of the DataFrame df from which you want to 
		extract values.
		* df[date_column] == x_value: This is a boolean condition. It checks which rows in the DataFrame 
		have a value in the column specified by date_column equal to the x_value (x-coordinate from the 
		mouse click event)
		* df[data][df[date_column] == initial_x_value]: This part filters the values in the column specified 
		by data where the corresponding date equals the x_value.
		* .values[0]: This extracts the first (and presumably the only) value from the resulting filtered 
		DataFrame. The condition 'df[date_column] == x_value' should iedally result in a single row, and 
		'.values[0]' retrieves the value from that row.

# 22. Syntax of 'annotate'
	The annotate method in matplotlib has the following syntax:
	'annotate(text, xy, xytext=None, xycoords='data', textcoords='data', arrowprops=None, annotation_clip=None, **kwargs)'
	Here's a breakdown of the important parameters:
		* text: The text of the annotation
		* xy: The point to annotate, specified as (x, y)
		* xytext: The position (x, y) to place the text at. If None, defaults to xy.
		* data: Uses the coordinate system of the data
		* axes fraction: Uses fractional coordinates of the axes.
		* figure fraction: Uses fractional coordinates of the figure.
		* textcoords: The coordinate system that xytext is given in. It has the same possible values as xycoords.
		* arrowprops: A dictionary of arrow properties. It can include properties like arrowstyle, connectionstyle,
		color, etc.
		* annotation_clip: If True, the annotation will only be drawn when the xy is within the axes.
		* **kwargs: Additional keyword arguments that are passed to the Text constructor for the next of the annotation.
# 23. text_annotation = f'{label}: {y_value_data:.2f} \n{filtered_data}Opt: {y_value_filtered:.2f}'
	'**.2f**' is a format specifier in Python used within f-strings or the str.format() method to control 
 	the formating of floating point numbers.
  		* '**.nf**': this specifies n digits after the decimal point
		* '**f**': Without a number after the dot, it defaults to displaying six digits after the decimal point.
