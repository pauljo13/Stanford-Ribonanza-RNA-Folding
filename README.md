# Stanford Ribonanza RNA Folding
### train_data.csv - the training data, with one experimental profile per row.
- sequence_id - (string) An arbitrary identifier like 8cdfeef009ea for each sequence.
- sequence - (string) Describes the RNA sequence, a string of A, C, G, and U.
- experiment_type - (string) Either DMS_MaP or 2A3_MaP to describe the type of chemical mapping experiment that was used to generate each profile. References: DMS, 2A3.
- dataset_name - (string) arbitrary name of high throughput sequencing dataset from which the reactivity profile was extracted.
- reads - (integer) Number of reads in the high throughput sequencing experiment that were assigned to the RNA sequence, and whose mutations were tabulated to compile the reactivity profile. (These values do not need to be predicted in this competition.)
- signal_to_noise - (float) Signal/noise value for the profile, defined as mean( measurement value over probed nts )/mean( statistical error in measurement value over probed nts). (These values do not need to be predicted in this competition.)
- SN_filter - (Boolean) 0 or 1 depending on whether the profile has signal_to_noise≥ 1.00 and reads≥ 100.* For evaluation, only sequences whose DMS_MaP and 2A3_MaP profiles both pass this filter will be used to score submissions. (These values do not need to be predicted in this competition.)
- reactivity_0001, reactivity_0002,… - (float) An array of floating point numbers of the train data, should have the same length as the RNA sequence, which defines the reactivity profile for the RNA. These are the type of data that need to be predicted in this competition. For sequences shorter than the maximum RNA length, positions that go beyond the sequence length have null. Several positions near the beginning and end of the sequence also cannot be probed due to technical reasons, and their reactivity values are null.
- reactivity_error_0001, reactivity_error_0002,… - (float) An array of floating point numbers, should have the same length as the corresponding reactivity_* columns, calculated errors in experimental values obtained in reactivity derived from counting statistics in the high-throughput sequencing experiment. (These values do not need to be predicted in this competition.)
*Note: Due to a minor bug, a few (<0.1%) profiles with reads under 100 are marked with SN_filter = 1, but this bug has been fixed for filtering profiles for private leaderboard scoring.

### sample_submission.csv - a sample submission file in the correct format.
This format is less compact than train_data.csv in that separate sequence positions are put on separate rows, which enables proper scoring with Kaggle’s MAE implementation.
- id - Integer (0,1,…) that identifies each sequence position in the sample submission. The sequences associated with each of these id values are provided in test_sequences.csv
- reactivity_DMS_MaP, reactivity_2A3_MaP - (float) Sample submission values (zero in example).

### test_sequences.csv - the test set sequences, without any columns associated with the ground truth.
- id_min, id_max - (integer) Minimum and maximum id values for the test sequence in a correctly formatted submission file (see sample_submission.csv).
- sequence_id - (string) An arbitrary identifier like eee73c1836bc for each test sequence.
- sequence - (string) Describes the RNA sequence, a string of A, C, G, and U, for which DMS and 2A3 reactivity needs to predicted and submitted in a file like sample_submission.csv.
- future - (Boolean) Sequences whose data will be collected after the start of the competition (but before final scoring) are labeled as 1.