# Impact Statement
The Impact Statement customization is a custom javascript plugin that runs with a default BBIS donation form.

##About the Customization

The Impact Statement customization will be driven from a management parameter that contains a range of values and Statements. When a donor indicates they will be giving a particular dollar amount the Impact Statement display text will dynamically update. The custom JavaScript will preform a “look up”. Once the appropriate range is located, the corresponding text string will be reflected in the Impact Statement customization.

### Library
A library of messages and range values must be used with the Impact Statement customization. Said library is a JSON object stored in a text file. A text file is used to make uploading to the BBIS Document Part a simple task - storing JSON is not possible at this time.

Each item or object in the library requires a message, rangeMax, rangeMin key and value pair. All “range" values (rangeMax and rangeMin) must be a floating point integer.

#### Libray JSON Example
    [
          {
               "message": "A message where the range min is 0.00 and range max is 99.99",
               "rangeMax" : 99.99,
               "rangeMin" : 0.00
          },
          {
               "message": "A message where the range min is 100.00 and range max is 499.99",
               "rangeMax" : 499.00,
               "rangeMin" : 100.00
          },
          {
               "message": "A message where the range min is 500.00 and range max is 999.99",
               "rangeMax" : 999.99,
               "rangeMin" : 500.00
          },
          {
               "message": "A message where the range min is 1000.00 and range max is 1000000000000",
               "rangeMax" : 1000000000000,
               "rangeMin" : 1000.00
          }
    ]


##Setup
### Library
The location of said library in the BBIS Documents part must be provided as an argument to the custom script at runtime. The user must upload the the JSON file to the BBIS Documents part. Once the file is uploaded, the file location must be passed.

*    Upload the “impactStatementLibrary.txt” to a BBIS Document Part
*    Make note of the URL
*    Provide the URL to the script as an argument at runtime

####Example
	jQuery('document').ready( function(){
		filelocation = {
			bbisDocumentURL : 'impactStatementLibrary.txt'
		});
	});


### Page Configuration
To install the customization into a BBIS page a user must add one (1) Unformatted Text and Images Part to a BBIS page. The Page must also contain one (1) BBIS Donation Form.

*    Create one (1) new Unformatted Text and Image Part
*    Add the following to said part
     <!—The Impact Statement JavaScript -->
     <script type="text/javascript" src=“impactStatement.js"></script>
     <!-- html element to be placed onto the page with a donation form -->
     <div id=“impactStatement"></div>
     
	<script>
		jQuery('document').ready( function(){
			// expected arguments are Federal Tax Rate + Provincial Tax Rate
			impactStatement(
				filelocation = {
					bbisDocumentURL : 'impactStatementLibrary.txt'
				}
			);
		});
	</script>
	

*    Add the part to a BBIS page in conjunction with a BBIS Donation Form

##Assumptions
*    United Way Toronto will be responsible for providing and managing impact Statements and corresponding range values
*    Text associated with each impact Statement should be free text - avoid embedding text into images