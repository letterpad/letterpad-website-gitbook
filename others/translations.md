# Translations

Letterpad uses react-18next library to handle translations. To add, edit or delete trannslation objects, you can use the below commands:

```bash
usage: yarn [operation] [options] [key=value || key]
    operation (Required):
        -a, --add     Add key value pair to all files
        -s, --set     Set value of an existing key in all files
        -d, --del     Delete key from all files
            --sync    Sync all files with en.json
    options (Optional)
        -en     Operation only on this file
        -fr     Operation only on this file
        -pl     Operation only on this file
```

```bash
# Adds the translated value, only in en.json and for others leave it blank.
yarn translate --add save="Save"

# Set the translated value only in en.json and for others, set the value to empty string.
yarn translate --set oldKey="New Value"

# sets a translation object in one file
yarn translate --set -en oldKey="New Value"

# deletes a translation object from all files
yarn translate --del save

# deletes a translation object from one file
yarn translate --del -en tags.title

# sync all files with en.json
yarn translate --sync
```

