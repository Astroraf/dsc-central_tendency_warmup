
# Summary Statistics Warmup

For this warmup, we will be parsing data held in objects returned from the Spotify API.  

![spotify](https://developer.spotify.com/assets/branding-guidelines/logo@2x.png)

# Task 1

The jazz_tracks object loaded above is a list of dictionaries. Each element of the dictionary contains data about a song. 

The first task is to parse this list, and gather the song length data from each dictionary.  

To do so, you will have to loop through jazz_tracks, use the appropriate key to access the song length data for each element, then append this data ponit to the list.  The list should then be composed of 1000 song lengths.


```python
track_durations = []
for track in jazz_tracks:
    track_durations.append(track['duration_ms'])
```

# Task 2

Now that you have the track durations of each jazz song stored in the track_durations list,  calculate the mean song length in our sample of tracks.

Don't use a built in operator, numpy, or the like.  Do it from scratch.



```python

track_total = 0
for track_length in track_durations:
    track_total += track_length
    
track_mean_length = track_total/len(track_durations)
```

# Task 3
Calculate the variance and standard deviation of the sample of track lengths. 

Since it is a sample, use the number of tracks minus 1 in the sample as the denominator.


```python

numerator = 0
denominator = len(track_durations) - 1
for track_length in track_durations:
    numerator += (track_length - track_mean_length)**2
    
track_length_variance = numerator/denominator
track_length_variance
```




    9000620195.035862




```python
track_standard_deviation = track_length_variance**.5
track_standard_deviation
```




    94871.59846358583



# Task 4: Covariance and correlation

The formula for covariance of a sample is  

$$s_{jk} = \frac{1}{n-1}\sum_{i=1}^{n}(x_{ij}-\bar{x}_j)(x_{ik}-\bar{x}_k)$$

Here are 4 lists variables taken from our Spotify API request.

Write a function that takes in any two of the 4 lists, and returns the covariance between them.


```python
def covariance(list_1, list_2):
    numerator = 0
    denominator = len(list_2)
    
    for x, y in zip(list_1, list_2):
        numerator += ((x - np.mean(list_1))*(y-np.mean(list_2)))
    
    return numerator/denominator

covariance(popularity, track_number)

```




    -19.825045999999972



The correlation between two array-like objects is simply the covariance divided by the product of the standard deviatiations of each list.

Write a function which calculates the correlation.  You can use the covariance function you calculated above within the correlation function.


```python

def correlation(list_1, list_2):
    
    return covariance(list_1, list_2)/(np.std(list_1)*np.std(list_2))

correlation(popularity, track_number)
```




    -0.32859477932496006



Using your function, of the four lists above, which have the strongest correlation?  Is the correlation positive or negative? What does this mean?

- Your written answer here

# Task 5:

Let's look at a histogram of the jazz track lengths.

Describe the shape of this histogram in the markdown cell below. Is it skewed? Which way? Does the mean you calculated above seem correct? Does it indicate the presence of outliers of song length?

- your answer here
>



```python
'''
The distribution of jazz lengths is right skewed. There appear to be a set of outliers 
representing songs of significantly longer length than the rest. Thse songs range from 600000 ms to over 800000 ms.
The mean we calculated above, 238829.013, seems to be appropriate, as it is visually just right of the peak of the histogram.
This makes sense given the right skew of the distribution.
'''
```




    '\nThe distribution of jazz lengths is right skewed. There appear to be a set of outliers \nrepresenting songs of significantly longer length than the rest. Thse songs range from 600000 ms to over 800000 ms.\nThe mean we calculated above, 238829.013, seems to be appropriate, as it is visually just right of the peak of the histogram.\nThis makes sense given the right skew of the distribution.\n'



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
    ax.hist(track_duration_list, bins=20)
    ax.set_title(f'{genre} Song Length')
    ax.set_xlabel('Song Length in MS');
    plt.show()
    
    print(f'''
    The mean track length of {genre} songs is {np.mean(track_duration_list)} ms.
    The variance of track lengths of {genre} songs is {np.var(track_duration_list)} ms.
    The standard deviation of track lengths of {genre} songs is {np.std(track_duration_list)} ms.
    
    
    ''')
    
    return [np.mean(track_duration_list), np.var(track_duration_list), np.std(track_duration_list)]
```

Use your function to compare track length statistics between classicle, rap, and punk songs.  
