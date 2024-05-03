Cohort-wise resting state EEG distribution
------------------------------------------

.. code-block:: python

		from almirah import Dataset

		import pandas as pd
		import seaborn as sns
		
		from mne.io import read_raw_edf

		dataset = Dataset(name='calmbrains')

		files = dataset.query(task='rest', datatype='eeg')

		print(f'number of files: {len(files)}')
		
		files.download()

		def calculate_mean_eeg(file):
		    """Return a DataFrame with average over all points and cohort as columns."""

		    raw = read_raw_edf(file.path)
		    mean_df = pd.DataFrame(
		        {
			    'mean': [raw.get_data().mean()],
			    'cohort': [file.get_tag('cohort')],
		        }
		    )

		    return mean_df

		df = pd.concat(map(calculate_mean_eeg, files), sort=False)
		df.head()

		sns.violinplot(data=df, x='mean', hue='cohort')
