
# Summary Statistics Warmup

For this warmup, we will be parsing data held in objects returned from the Spotify API.  

![spotify](https://developer.spotify.com/assets/branding-guidelines/logo@2x.png)


```python
import requests
import json
import numpy as np
import matplotlib.pyplot as plt
import pickle
```


```python
with open('data/jazz_query_response', 'rb') as read_file:
    jazz_tracks = pickle.load(read_file)
```

# Task 1

The jazz_tracks object loaded above is a list of dictionaries. Each element of the dictionary contains data about a song. 

The first task is to parse this list, and gather the song length data from each dictionary.  

To do so, you will have to loop through jazz_tracks, use the appropriate key to access the song length data for each element, then append this data ponit to the list.  The list should then be composed of 1000 song lengths.


```python
# Your code here
track_durations = None
```

# Task 2

Now that you have the track durations of each jazz song stored in the track_durations list,  calculate the mean song length in our sample of tracks.

Don't use a built in operator, numpy, or the like.  Do it from scratch.



```python
# Your code here
track_mean_length = None
```


```python
print(f'The average track length is {track_mean_length} ms')
```

    The average track length is 238829.013 ms



```python
# Cross check with numpy
np.mean(track_durations)
```




    238829.013



# Task 3
Calculate the variance and standard deviation of the sample of track lengths. 

Since it is a sample, use the number of tracks minus 1 in the sample as the denominator.


```python
# Your code here
track_length_variance = None
```


```python
# Cross check with numpy.  ddof stands for degrees
np.var(track_durations, ddof=1)
```




    9000620195.035866




```python
# Your code here
track_standard_deviation = None

```


```python
# Cross check with numpy
np.std(track_durations, ddof=1)
```




    94871.59846358585



# Task 4: Covariance and correlation

The formula for covariance of a sample is  

$$s_{jk} = \frac{1}{n-1}\sum_{i=1}^{n}(x_{ij}-\bar{x}_j)(x_{ik}-\bar{x}_k)$$

Here are 4 lists variables taken from our Spotify API request.


```python
popularity = [track['popularity'] for track in jazz_tracks]
duration = [track['duration_ms'] for track in jazz_tracks]
total_tracks = [track['album']['total_tracks'] for track in jazz_tracks]
track_number =  [track['track_number'] for track in jazz_tracks]
```

Write a function that takes in any two of the 4 lists, and returns the covariance between them.


```python
# Your code here
def covariance():
    pass
```

The correlation between two array-like objects is simply the covariance divided by the product of the standard deviatiations of each list.

Write a function which calculates the correlation.  You can use the covariance function you calculated above within the correlation function.


```python
# Your code here
def correlation():
    pass
```

Using your function, of the four lists above, which have the strongest correlation?  Is the correlation positive or negative? What does this mean?

- Your written answer here

# Task 5:

Let's look at a histogram of the jazz track lengths.


```python
# Don't worry about the matplotlib syntax yet
fig, ax = plt.subplots()
ax.hist(track_durations, bins=20)
ax.set_title('Jazz Song Length')
ax.set_xlabel('Song Length in MS');
```


![png](index_files/index_29_0.png)


Describe the shape of this histogram in the markdown cell below. Is it skewed? Which way? Does the mean you calculated above seem correct? Does it indicate the presence of outliers of song length?

- your answer here
>


# Task 6

Now, let's write a function that takes in any list of track lengths, then prints and returns the mean, variance, and standard deviation of the list.

Feel free to use numpy or other methods to calculate the statistics.

As a bonus, the function is pre-coded to print out a histogram as well.


```python
def track_length_descriptor(track_duration_list, genre=''):
    
    '''
    Params
    ______
    track_duration_list: a list of track lengths in milliseconds 
    returned from the spotify API
    
    genre: a string to add genre to the histogram title.
    
    Returns
    _______
    a list containing the mean, variance, and standard deviation of the tracks
    
    '''
    
    fig, ax = plt.subplots()
    ax.hist(<fill_in>, bins=20)
    ax.set_title(f'{genre} Song Length')
    ax.set_xlabel('Song Length in MS');
    plt.show()
    

```


      File "<ipython-input-42-e2c99dd6d74f>", line 18
        ax.hist(<fill_in>, bins=20)
                ^
    SyntaxError: invalid syntax




```python
with open('data/track_length_lists', 'rb') as read_file:
    classical_track_durations, rap_track_durations, punk_track_durations = pickle.load(read_file)
```

Use your function to compare track length statistics between classicle, rap, and punk songs.  


```python
track_length_descriptor(classical_track_durations, "Classical")
```


![png](index_files/index_36_0.png)


    
        The mean track length of Classical songs is 165906.707 ms.
        The variance of track lengths of Classical songs is 12858950170.405153 ms.
        The standard deviation of track lengths of Classical songs is 113397.31112511069 ms.
        
        
        





    [165906.707, 12858950170.405153, 113397.31112511069]




```python
track_length_descriptor(rap_track_durations, 'Rap')
```


![png](index_files/index_37_0.png)


    
        The mean track length of Rap songs is 202687.558 ms.
        The variance of track lengths of Rap songs is 2652897639.9546356 ms.
        The standard deviation of track lengths of Rap songs is 51506.28738275198 ms.
        
        
        





    [202687.558, 2652897639.9546356, 51506.28738275198]




```python
track_length_descriptor(punk_track_durations, 'Punk')
```


![png](index_files/index_38_0.png)


    
        The mean track length of Punk songs is 216115.196 ms.
        The variance of track lengths of Punk songs is 3202906042.827584 ms.
        The standard deviation of track lengths of Punk songs is 56594.22269832482 ms.
        
        
        





    [216115.196, 3202906042.827584, 56594.22269832482]


