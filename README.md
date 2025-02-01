README
Bitcoin Private Key Brute Forcing Tool
This Python tool uses a brute-force approach to derive Bitcoin private keys and their associated addresses. The tool searches within a given range of private keys and compares the derived addresses against a list of target addresses provided in a file (challenge.txt). If a match is found, the tool saves the corresponding private key and address to a results file (I_win.txt).

Features
Brute-force Search: The tool generates private keys from a specified range and derives Bitcoin addresses.
Multiple Address Types: Supports derivation of Bitcoin addresses in different formats including P2PKH (Pay-to-PubKey-Hash) and Bech32 (SegWit).
Multiprocessing: Optimized for multi-core processors, using Python's multiprocessing module to distribute the workload across multiple CPU cores.
Progress Reporting: Shows a progress bar using the tqdm library to indicate the current status of the search.
Results Saving: Saves found addresses and corresponding private keys to a file (I_win.txt).
Requirements
To run this tool, you'll need the following Python libraries:

ecdsa for elliptic curve cryptography (used for key generation and verification).
base58 for encoding Bitcoin addresses.
bech32 for SegWit address generation.
tqdm for progress bar display.
hashlib (comes with Python) for hash functions.
multiprocessing (comes with Python) for parallel processing.
You can install the required libraries using pip:

bash
Copy
pip install ecdsa base58 bech32 tqdm
Setup Instructions
Prepare the target addresses file:

Create a file named challenge.txt and populate it with the Bitcoin addresses you want to search for (one address per line).
Run the tool:

Open a terminal or command prompt.
Navigate to the directory where the Python script (force.py) is located.
Execute the script by running:
bash
Copy
python force.py
The script will start searching for matching Bitcoin private keys and addresses.

Detailed Description
load_targets(file_path)
Description: Loads target Bitcoin addresses from the specified file (challenge.txt). The addresses are read into a set for efficient lookup.
Parameters:
file_path: Path to the file containing target addresses.
Returns: A set of target Bitcoin addresses.
save_results(file_path, found_data)
Description: Saves the found addresses and corresponding private keys to the specified file (I_win.txt).
Parameters:
file_path: Path to the file where results will be saved.
found_data: List of tuples containing found addresses and their corresponding private keys.
derive_address(private_key_hex)
Description: Derives Bitcoin addresses from a given private key in hexadecimal format. Supports both P2PKH and Bech32 addresses.
Parameters:
private_key_hex: The private key in hexadecimal format.
Returns: A tuple containing the P2PKH address and Bech32 address.
brute_force_worker(start, end, targets, result_queue)
Description: The worker function that runs in parallel. It generates private keys in the given range, derives the corresponding Bitcoin addresses, and checks for matches against the target addresses. Found addresses are placed into the result queue.
Parameters:
start: Starting value of the private key range.
end: Ending value of the private key range.
targets: Set of target Bitcoin addresses.
result_queue: Queue to collect results of found addresses and their private keys.
brute_force(targets)
Description: Main brute-force function. Divides the work into chunks based on the number of available CPU cores and runs the worker function in parallel. Progress is tracked using the tqdm progress bar.
Parameters:
targets: Set of target Bitcoin addresses.
Returns: A list of found addresses and private keys.
Notes
Private Key Range: The range of private keys to search through is fixed, but you can adjust the PRIVATE_KEY_RANGE_START and PRIVATE_KEY_RANGE_END constants if needed.
Performance: The script uses all available CPU cores to perform the search. If you want to limit the number of cores, you can adjust the num_processes value in the brute_force function.
Efficiency: This brute-force search can take significant time and computational power, especially if the target addresses are far apart in the private key space.
Example Output
sql
Copy
Starting optimized search for Bitcoin private keys...
Searching: 100%|██████████████████████| 100000000/100000000 [01:23<00:00, 1200000.00 keys/s]
Search completed! Time Taken: 83.56 seconds
The found private keys and addresses will be saved to I_win.txt in the format:
vbnet
Copy
Address: 1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa, Private Key: 5Jp6mM6t5wYsNpXvkGLyMX5Ty39gQjJtpXRG5Nrw5o2P2Q6VNkf
Address: bc1qar0srrr7v6cmh5m8hdvkf3gje5xn8tk6y9v4lt, Private Key: 5Jp6mM6t5wYsNpXvkGLyMX5Ty39gQjJtpXRG5Nrw5o2P2Q6VNkf
License
This tool is for educational and research purposes only. Use it responsibly.



