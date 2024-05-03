Cohort-wise Hippocampus to Total Brain Volume ratio distribution
================================================================

.. code-block:: python

		from almirah import Dataset

		import numpy as np
		import pandas as pd
		import seaborn as sns

		files = dataset.query(pipeline='smriprep', filename='aseg', extension='.stats')

		def extract_brain_vol(file):
		    """Returns brain stats from smriprep output stats.
		    From: https://github.com/nipy/nibabel/issues/513
		    """

		    stats_df = pd.DataFrame(
		        np.loadtxt(file.path, dtype="i1, i4, i4, f4, U32, f4, f4, f4, f4, f4"),
                        columns=["f4", "f3"],
                    ).T

		    header, stats_df = stats_df.iloc[0], stats_df[1:]
                    stats_df.columns = header
		    
                    stats_df["cohort"] = file.get_tag('cohort')

		    return stats_df

		df = pd.concat(map(extract_brain_vol, files), sort=False)
		df.head()

		sns.violinplot(data=df, x='ratio', hue='cohort')
