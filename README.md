# Prerequisite

Ansible 2.8

# Overview

This ansible playbook can be used for processing a given CtC test dataset in CSV format. The test result for each entry can be one of the following 4 values:

- OK: the test is successful 
- FAILED: test is considered failed when the returned data does not match expectation
- ERROR: not able to get a valid response from the target backend
- SKIPPED: the entry's bank id is not valid 

Example output:
```
ok: [localhost] => {
    "testResults": {
        "2000085698": "OK",
        "2000086124": "OK",
        "2000099037": "OK",
        "2000102848": "OK",
        "2000118854": "OK",
        "2000133634": "OK",
        "2000136222": "OK",
        "2000139230": "OK",
        "2000167352": "OK",
        "2000176986": "OK",
        "2000182699": "SKIPPED",
        "2000194697": "OK",
        "2000201800": "OK",
        "2000230469": "OK"
    }
}
```


# How to run

The target backands and the respective bank IDs need to be defined in vars.yaml in the following format:
```
peers:
  - name: bank 1
    id: XXXXXX
    backend: http://1.1.1.1:11111
  - name: bank 2
    id: YYYYYY
    backend: http://2.2.2.2:22222
```
To run the playbook:
```
# this expect an input file named 'input.csv' in the same directory
ansible-playbook test.yaml

# alternatively, provide the input file as 
ansible-playbook test.yaml -e 'inputFile=/tmp/testdata.csv'
```


