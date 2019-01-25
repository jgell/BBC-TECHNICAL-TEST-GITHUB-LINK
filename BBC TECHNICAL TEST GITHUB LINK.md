#  BBC TECHNICAL TEST GITHUB LINK


Full code below unfortunatly Markdown has no syntax highlighting for matlab. <br>
Images and explinations are offered below with a video link.

### Matlab Code

```

close all
clear all
clc
hold all

%generate a table of states being either 0 or 1
Params = 100;
delay = 0.1; %slow down frame rate in seconds
X = Params; %number of rows
Y = Params; %number of columns
%rand function will create uniformly distributed random numbers between 0 - 1
Table = rand(X,Y) > 0.7; %generate a percentage of grid to be live or dead.
Transition_table = zeros(X,Y); %store a updating table until a full transition is needed 
figure(1); %create window to display grid
imagesc(Table); %display image with scaled colours
axis image; %scale image axis
colormap('gray'); %convert to black and white pixels

%generate infinite while loop
while true
Filtered_table = zeros(X,Y);
    %outter 2 for loops will cycle through every element of the matrix
    for j=1:1:X
        for i=1:1:Y
             %2 for loops will cycle through a 3X3 matrix around element
            for inc_j=-1:1:1
                for inc_i=-1:1:1
                    x = j + inc_j;
                    y = i + inc_i;
                    
                    %When exceeding X parameter wrap to otherside of matrix
                    if  x == X+1
                        x = 1;
                    elseif x == 0  
                        x = X;
                    end
                    
                    %When exceeding Y parameter wrap to otherside of matrix
                    if  y == Y+1
                        y = 1;
                    elseif  y == 0
                        y = Y;
                    end
                    %sum of elements
                    Filtered_table(j,i) = Filtered_table(j,i) + Table(x,y);
                end
            end
        end
    end
    
    %sum of 9 elements subtract table to correct the filtered matrix
    Filtered_table = Filtered_table-Table;
    
    %outter 2 for loops to cycle through every element
    for i=1:1:X
        for j=1:1:Y
            %if element is alive
            if Table(i,j) == 1
                switch Filtered_table(i,j)
                    case 0 %scenario 1
                        Transition_table(i,j) = 0;
                    case 1 %scenario 1
                        Transition_table(i,j) = 0;
                    case 2 %scenario 3
                        Transition_table(i,j) = 1;
                    case 3 %scenario 3
                        Transition_table(i,j) = 1;
                    otherwise %scenario 2
                        Transition_table(i,j) = 0;
                end
            end
            %if element is not alive
            if Table(i,j) == 0
                if Filtered_table(i,j) == 3 %scenario 4
                    Transition_table(i,j) = 1;
                end
            end
        end
    end
    
    Table = Transition_table; %replace overwrite table with new matrix
    imagesc(Table); %display new states to figure
    pause(delay); %delay between states
end

```
<br>
<br>

### code broken down with methods explained

<br>
<br>

This is the initialisation of section before entering an infinite while loop.
I have tried to make the code dynamic so that adjustment can be done within this block of code.


<br>
<br>

![](https://scontent-lhr3-1.xx.fbcdn.net/v/t1.0-9/50494107_723289084752718_4593368060219359232_n.jpg?_nc_cat=104&_nc_ht=scontent-lhr3-1.xx&oh=6e6246cf9a35a29b6ca3c34f4efe5a87&oe=5CF64085)

<br>
<br>

To make the environment infinite we need to allow for the elements on the edges
of the matrix wrap round to the other side. This set of nested for loops will allow
for this by summing a 3 by matrix that has a isolated element in the middle.
When a boundary is exceeded no complex math is needed as program is only sampling one element
away from the centre.
<br>
<br>
On the very last line of code within this image the original table needs to be
subtracted from the filtered one as we have summed 9 elements opposed to the 8
that was supposed to. The table is made of zeros and ones and as matrix addition and
subtraction is done elementwise this method is allowed.

<br>
<br>

![](https://scontent-lhr3-1.xx.fbcdn.net/v/t1.0-9/50507974_723289058086054_5557158047131893760_n.jpg?_nc_cat=107&_nc_ht=scontent-lhr3-1.xx&oh=97c0d6d6aae809bfcc6fc17a8ca0628d&oe=5CB70306)

<br>
<br>

Now that every state in the matrix has been replaced by the number of live
cells around it, each cell can be assessed, and each matrix element will be changed
to boolean values dependant on the outcome of the scenarios.

<br>
<br>

![](https://scontent-lhr3-1.xx.fbcdn.net/v/t1.0-9/50636621_723289054752721_4686612440165646336_n.jpg?_nc_cat=103&_nc_ht=scontent-lhr3-1.xx&oh=2de6db32bd5547ebf20279040e2de217&oe=5CC2BE01)

<br>
<br>

Set the value of Table equal to the transition matrix for the next generation to run.

<br>
<br>

![](https://scontent-lhr3-1.xx.fbcdn.net/v/t1.0-9/50519814_723289051419388_6168212415952453632_n.jpg?_nc_cat=107&_nc_ht=scontent-lhr3-1.xx&oh=4770ab9eb5afb144b23cc0534cc7f305&oe=5CB4A0F1)

### Video link

[![](https://scontent-lhr3-1.xx.fbcdn.net/v/t1.0-9/50532313_723315968083363_1165381101653327872_o.jpg?_nc_cat=100&_nc_ht=scontent-lhr3-1.xx&oh=a14a0cfba8786e952e44e06a4e460f9c&oe=5D008932)](https://www.facebook.com/jack.gell.39/videos/a.722619064819720/723311508083809/?type=3)
