# Basics :

You can save variables that are accessible to any `script(.m) or livescript(.mlx)` in a `.mat` file and access it anywhere.
```matlab
% save var1, var2, to a .mat file:
save('datafile.mat', 'var1', 'var2', ....);

% save all variables in workspace to .mat file:
save datafile.mat;

% Append new variable to the file:
save('datafile.mat', 'varNew', '-append');

% load variables form .mat file:
load datafile;

% load a specific variable from a mat file:
load('datafile.mat', 'variableName');
```
---
### Array :
```matlab
% generate numbers in a range with specific amount of break btwn 2 elements:
x = [start_element:break_btwn_2_elements:end_element];


% generate n random numbers in a range:
x = linspace(start_element, end_element, number_of_elements);


x = [1:5]
% generates x = [1,2,3,4,5];
x = x' 
% generates x = [1
%                2
%                3
%                4
%                5]


y = rand(row,col)
% generates [row x col] matrix with random values from range 0 to 1, values are taken from uniform distribution


z = zeros(row,col)
% generate [row x col] matrix of all elements as '0'


z = ones(row,col)
% generate [row x col] matrix of all elements as '1'


z = data(end-1,3)
y = data(end,3)
% gives back last row 3rd column element of data matrix


x = A(:,1)
% returns an array of all row elements in column 1


volumes = data(:,end-1:end)
% returns last two columns of data matrix


vr = round(va);
% round off a value


mass = density.*va ;
% element-wise multiplication


[row, col] = size(data)
% returns numbers of elements in row and col


[vMax, ivMax] = max(v2);
% returns the maximum element and its index in an array


z = v1(v1 < 4)
% returns all elements less than 4 in v1


a = sample(v1 < 4)
% contains the elements of sample corresponding to where v1 is less than 4.
```
---
### Plot :
```matlab
plot(sample, mass2, "r *")
% plot a graph with sample on x-axis and mass2 on y-axis
% and r ==> red line
% " " ==> space in between means don't drae line just plot points
% * ==> means point co-ordinnates with * mark


plot(x,y,"r--o")
% plots a red (`r`) dashed (`--`) line with circle (`o`) markers


plot(x1,y1)  
hold on  
plot(x2,y2)
% plots both points on same graph


hold off
% removes the hold on a graph so a new graph can be made


title("Plot Title")
% add title to plot


ylabel("Y-Axis Label")
% add label to y axis


legend("Exp A","Exp B")
% add legend to show which line/point represent which value of data
```
---
