# Identity Forge

This project is a Python command-line tool that generates a specified number of fictitious identities (including name, surname, username, and email address) from a provided list of names and surnames. The generated identities are saved in CSV or Excel (XLSX) format, ensuring that all usernames are unique.

## Features

- Generates unique usernames based on name and surname combinations.
- Optionally uses the `faker` library to generate random names if no input file is provided.
- Outputs identities in both CSV and Excel formats.
- Ensures there are no duplicate usernames and emails.
- Command-line arguments allow flexible input and output options.

## Prerequisites

Before running the project, ensure you have the following installed:

- Python 3.8+
- `pandas` library (for CSV/Excel/JSON/Parquet export)
- `argparse` library (for parsing command-line arguments)
- `faker` library (for generating random names if no input file is provided)
- `pytest` library (for testing)
- `unidecode` library (for reducing Unicode to an ASCII representation)
- `aiofiles` library (for asynchronous file operations)

You can install these libraries manually via `pip`:

```bash
pip install pandas argparse unidecode faker aiofiles
```

Or by using `requirements.txt` file:

```bash
pip install --prefix=/install -r ./requirements.txt
```

## Usage
### Command-Line Arguments

You can specify the number of identities to generate, the input file, and the output format and more through command-line arguments.

```bash
python src/main.py <number_of_identities> [--names-file NAMES_FILE] [--surnames-file NAMES_FILE] [--output-file OUTPUT_FILE] [--output-format {csv,excel,json,parquet,all}]
```

### Command-Line Arguments

To generate 100 identities from a given names file and save them as CSV, JSON, Parquet and Excel (all is default):

```bash
python src/main.py 100 --names-file names.txt --surnames-file surnames.txt --output-file output/identities --output-format all
```

If no --names-file/--surnames-file argument is given, the tool will use the faker library to generate random names and surnames:

```bash
python identity_generator.py 100
```

### Arguments

- number_of_identities: The number of identities to generate (required).
- --names-file: Optional file containing the list of names and surnames (if not provided, random names will be generated using the faker library).
- --surnames-file: Optional file containing the list of names and surnames (if not provided, random names will be generated using the faker library).
- --output-file: Path to save the output file without extension (default is output/identities). The appropriate extension (.csv or .xlsx) will be added based on the --output-format.
- --output-format: Output format, either csv, excel, or both (default is both).
- --workers: Allows users to specify the number of parallel workers (CPU cores) to use. Defaults to 4.

### Input File Format

The input file (surnames.txt) should contain surnames, one per line, like this:

```bash
John
Jane
```

The input file (names.txt) should contain names, one per line, like this:

```bash
Doe
Smith
```

The program will randomly combine these names and surnames to create identities.

## Output

The generated output will include the following columns:

```bash
username
password
email
isEmailVerified
name
surname
middlename
honorific
language
isActive
gender
communicationChannel
addressType
streetNumber
complementStreetNumber
streetType
streetName
complementLocation
complementIdentification
complementAddress
postalCode
locality
region
country
```

Each generated identity includes detailed address information, broken down into multiple columns:

- **Type**: Either "work" or "home".
- **StreetNumber**: The building or street number.
- **ComplementStreetNumber**: Additional street number information like "bis" or "ter" (optional).
- **StreetType**: Type of street (e.g., avenue, boulevard).
- **StreetName**: The name of the street.
- **Locality**: The city or town.
- **ComplementLocation**: Additional location information (optional).
- **ComplementIdentification**: Identification complements (optional).
- **ComplementAddress**: Additional address details such as apartment or suite number.
- **Region**: The region in France (e.g., Île-de-France).
- **Country**: Always "France".
- **PostalCode**: The postal code of the address.

## License

This project is licensed under the Apache License, Version 2.0.
