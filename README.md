# CiviCRM Message Template Merge API

Provides a "merge" action on the MessageTemplate API, to allow programmatic
execution of the "Print/Merge Document" functionality for a given contact.

## Usage:

```
civicrm_api3('MessageTemplate', 'merge', $params);
```

## API parameters for MessageTemplate.merge:

* `msg_template_id`: (Int) **Required**. Value of `civicrm_msg_template.id` for
  desired template. If no such message template exists, an exception is thrown.
* `contact_id`: (Int) **Required**. Value of `civicrm_contact.id` for desired
  contact. If no such contact exists, an exception is thrown.
* `pdf_format_id`: (Int) **Optional**. Value of `civicrm_option_value.value` for
  the desired option in the 'PDF Formats' option group. If omitted, the Default
  format is used. If given and no such PDF format exists, an exception is thrown.
* `source_contact_id`: **Optional**. Value of contact.id for contact to be
  recorded as the creator of the corresponding "Print PDF Letter" activity. If
  not given, the current logged in user is used. If no such contact exists, no
  activity is created.
* `document_type`: (String) **Optional**. **Experimental**: Currently this is ignored
  and the value \'pdf\' is always used. One of: \'pdf\', \'docx\', \'odt\',
  \'html\'. Defaults to \'pdf\'.

## API result for MessageTemplate.merge:
This API, like CiviCRM native "Print/Merge Document" functionalty, will create
a temporary file containing the merged contents in the appropriate file format.

A successful API call will include the temporary filename:
```
{
    "is_error": 0,
    "version": 3,
    "count": 1,
    "id": 0,
    "values": [
        {
            "tmp_file_name": "/tmp/ConsoleTee-6APMdp",
            "activity_id": 766
        }
    ]
}
```
