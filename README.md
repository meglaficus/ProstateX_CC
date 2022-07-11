# ProstateSeg_QC


ProstateSeg_QC is a quality control algorithm to fix prostate zone segmentation masks. It finds and rectifies common errors that occur during manual segmentation.

## Method

This is an all-in-one algorithm to process the entire dataset. It is largely based on finding and analyzing connected components.

The algorithm requires separate files for the whole prostate mask, the peripheral zone mask and the non-peripheral (central) zone mask. Here is what it does:
- Finds and removes all small connected components from all the masks.

![Example 1](examples/filter.jpg)


- Finds and patches all small holes in the masks.

![Example 2](examples/hole_in_center.jpg)


- Finds snippets that are labeled as central zone but were very clearly just small errors when marking the peripheral zone mask onto the whole prostate mask. It converts those to peripheral zone.

![Example 3](examples/snippet_red.jpg)


- Checks if the whole mask equals the sum of the peripheral and central zone masks. If not, it replaces the whole mask.


## Requirements

The program requires these modules to be installed:

- numpy
- pandas
- SimpleITK
- connected-components-3d
- tqdm
- regex


## Usage

First clone or fork repo. Then open main.py and enter the paths to relevant directories at top of file as shown bellow. Then just run main.

```python
WHOLE_PATH = '/<example path>/whole'
PERIPHERAL_PATH = '/<example path>/peripheral'
CENTRAL_PATH = '/<example path>/central'
```
By default the program saves only the masks that were changed, saving them into new directories that are created in the cwd. It also creates .csv files that store the information on all the errors that were found.

If you are working with masks files where there is a single mask file for both zones do not fret! This is why 'tools/separate_masks.py' is for. If you want to join the masks back together, use 'tools/join_masks.py' .

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
