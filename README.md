> fork to use github.com/GuoxiW/media-protocol/oip042
> https://oip.wiki/Research-Tomogram

# Media-Protocol

[![Build Status][TravisSVG]][TravisLink] [![Coverage Status][CoverallsSVG]][CoverallsLink] [![Go Report Card][GoReportCardSVG]][GoReportCardLink]
## OIP-042 JSON Standards
The following are the current OIP-042 JSON Standards.
```javascript
 {
 	"oip042": {
 		"publish": {
 			"artifact": {
 				"floAddress": "string",
 				"timestamp": ten digit integer,
 				"type": "Research",
 				"subtype": "Tomogram",
 				"details": {
 					"title": "string",
 					"description": "string",
 					"date": ten digit integer,
 					"etdbid": "string",
 					"artNotes": "string",
 					"scopeName": "string",
 					"speciesName": "string",
 					"strain": "string",
 					"NBCItaxID": "string",
 					"tiltSingleDual": "string",
 					"defocus": "string",
 					"magnification": "string",
 					"swAcquisition": "string",
 					"swProcess": "string",
 					"emdb": "string",
 					"tags": "comma delimited list of search terms",
 					"extraInfo": {
 						
 					}
 				"roles": [
 				  {
 					"party": "tenure",
 				  },
 				  {
 					"party": "tenure",
 				  } 
 				],
 				"storage": {
 					"network": "string",
 					"location": "string",
 					"files": [
 						{
 							"fName": "string",
 							"fType": "string",
 							"fSize": integer,
 							"fNotes": "string",
 							"dName": "string"
 						}
 					]
 				},
 				"signature": "string"
 			}
 		}
 	}
 }
 ```

 - Introduction
 ```
  artifact.floAddress		... The FLO txid that published this artifact
 artifact.timestamp		... UNIX timestamp
 artifact.type			... "Research"
 artifact.subType		... "Tomogram"
 artifact.details.
 	title			... Default to species name
 				''TiltSeriesData:title''
 	description		... Optional descriptive text. This may be
 					used for application formatted data. Set
 					to empty string if no description is available.
 	date			... unixtime of original publish date
 				''TiltSeriesData:tomo_date''
 	etdbid			... ID from caltech's internal db
 				''AcquisitionData:DEF_id''
 	artNotes		... Notes for the snapshots.
 				''AcquisitionData:TXT_notes'' & ''ScopeData:TXT_notes'' & ''SpeciesData:TXT_notes'' & ''TiltSeriesData:TXT_notes''
 	scopename		... Name of scope?
 				''ScopeData:scopename''
 	speciesName		... Name of species
 				''SpeciesData:SpeciesName''
 	strain			... Name of strain
 				''SpeciesData:strain''
 	NBCItaxID		... NBCI taxonomy ID
 				''SpeciesData:tax_id''
 	tiltSingleDual		... tilited in one axis or two axes
 				''TiltSeriesData:single_dual''
 	defocus			... ?
 				''TiltSeriesData:defocus''
 	magnification		... ?
 				''TiltSeriesData:magnification''
 	scope			... ?
 				''TiltSeriesData:scope''
 	swAcquisition		... type of software to acquire the tilt series
 				''TiltSeriesData:software_acquisition'''
 	swProcess		... type of processing used to build reconstruction
 				''TiltSeriesData:software_acquisition'''
 	emdb			... code for the tomogram if is also on EMDB database
 				''TiltSeriesData:emdb'''
 	tags			... Optional comma delimited list of search terms.
 artifact.roles.
 	party			... who did what
 				''GroupData:name'' (w/ tenure "Lab) & ''UserData:fullname'' (w/ tenure "Microscopist") & ''TiltSeriesData:roles'' 
 	tenure			... what they did [examples are Lab, Institution, Microscopist] 
 				''TiltSeriesData:roles''
 artifact.storage.
 	network			... Name of the storage network. For the Electro Tomography DB, it is IPFS.
 	location		... IPFS directory location hash
 	files			... Array of file descriptions. These files provide the sources for this
 					artifact. These can be documents, audio, video, or other binary data
 					that represent any supporting evidence for this artifact. Additionally,
 					the files themselves can contain cryptographic proofs without the
 					original content providing a mechanism for privacy where original
 					documents are stored off-chain.
 		fType		... There are a limited set of file types in a Tomogram artifact. They
 					are: "tiltSeries", a .mrc or .st file, tomogram "reconstruction", a .rec or .mrc 
 					file, "subvolume", a cropped reconstruction .rec or .mrc 
 					file, "snapshot" a .jpg or a .png file, and "preview" a .flv (for now) file.
 				if ''ThreeDFile:classify'' == 'rawdata', then "tiltSeries"
 				if ''ThreeDFile:classify'' == 'reconstruction', then "reconstruction"
 				if ''DataFile:filetype'' == '2dimage', then "snapshot"
 				if ''DataFile:filetype'' == 'movie', then "preview"
 		fName		... Filename
 				''DataFile:filename''
 		fSize		... File size in bytes
 		fNotes		... Notes for this file in particular (applicable mainly to snapshots)
 				''DataFile:TXT_notes'' 
 		dName		... Optional display name used by user interfaces
 artifact.signature		... Signature signed by publisher

```




## OIP-041 JSON Standards
The following are the current OIP-041 JSON Standards.

### Publish Artifact
```javascript
{  
    "oip-041":{  
        "artifact":{  
            "publisher":"$PublisherAddress",
            "timestamp":1234567890,
            "type":"$ArtifactType",
            "info":{  
                "title":"$ArtifactTitle",
                "description":"$ArtifactDescription",
                "year":1234,
                "extraInfo":{  
                    "artist":"$Creator",
                    "company":"$Distributor",
                    "composers":[  
                        "$Composer1",
                        "$Composer2"
                    ],
                    "copyright":"",
                    "genre","$genreFromList"
                    "usageProhibitions":"",
                    "usageRights":"",
                    "tags":[  
                        "$ArtifactTag1",
                        "$ArtifactTag2"
                    ]
                }
            },
            "storage":{  
                "network":"IPFS",
                "location":"$IPFSAddress",
                "files":[  
                    {  
                        "disallowBuy":true,
                        "dname":"$DisplayName",
                        "duration":123,
                        "fname":"$FileName",
                        "fsize":123,
                        "minPlay":"$minPlayPriceUSD",
                        "sugPlay":"$suggestedPlayPriceUSD",
                        "promo":"$CutForPromoterSales",
                        "retail":"$CutForPlatformSales",
                        "ptpFT":12,
                        "ptpDT":34,
                        "ptpDA":56,
                        "type":"$MediaType",
                        "tokenlyID":"$SongTokenlyID"
                    },
                    {  
                        "dissallowPlay":true,
                        "dname":"$DisplayName",
                        "duration":123,
                        "fname":"$FileName",
                        "fsize":123,
                        "minBuy":"$minBuyPriceUSD",
                        "sugBuy":"$suggestedBuyPriceUSD",
                        "promo":"$CutForPromoterSales",
                        "retail":"$CutForPlatformSales",
                        "type":"$MediaType",
                        "tokenlyID":"$SongTokenlyID"
                    },
                    {  
                        "dname":"$DisplayName",
                        "duration":123,
                        "fname":"$FileName",
                        "fsize":123,
                        "minPlay":"$minPlayPriceFiat",
                        "sugPlay":"$suggestedPlayPriceFiat",
                        "minBuy":"$minBuyPriceFiat",
                        "sugBuy":"$suggestedBuyPriceFiat",
                        "promo":"$CutForPromoterSales",
                        "retail":"$CutForPlatformSales",
                        "ptpFT":12,
                        "ptpDT":34,
                        "ptpDA":56,
                        "type":"$MediaType",
                        "tokenlyID":"$SongTokenlyID"
                    },
                    {  
                        "dname":"Cover Art",
                        "fname":"$CoverArtFilename",
                        "fsize":123,
                        "type":"coverArt",
                        "storage":{  
                            "network":"HTTP",
                            "location":"$ThumbnailURL"
                        }
                    }
                ]
            },
            "payment":{  
                "fiat":"$fiat_id",
                "scale":"1000:1",
                "sugTip":[  
                    123,
                    123,
                    123
                ],
                "tokens":{  
                    "btc":"$BitcoinAddress",
                    "early":"",
                    "mtmcollector":"",
                    "mtmproducer":"",
                    "happybirthdayep":"",
                    "ltbcoin":""
                }
            },
            "varID":""
        },
        "signature":"$IPFSAddress-$PublisherAddress-$timestamp"
    }
}
```
#### Supported Genres
There are currently four different lists that you can select Genres from.
##### Web Videos
```javascript
[
	"Autos & Vehicles",
	"Film & Animation",
	"Music",
	"Pets & Animals",
	"Sports",
	"Short Movies",
	"Travel & Events",
	"Gaming",
	"Videoblogging",
	"People & Blogs",
	"Comedy",
	"Entertainment",
	"News & Politics",
	"Howto & Style",
	"Education",
	"Science & Technology",
	"Nonprofits & Activism",
	"Movies",
	"Anime/Animation",
	"Action/Adventure",
	"Classics",
	"Comedy",
	"Documentary",
	"Drama",
	"Family",
	"Foreign",
	"Horror",
	"Sci-Fi/Fantasy",
	"Thriller",
	"Shorts",
	"Shows",
	"Trailers"
]
```
##### Movies
```javascript
{
	"Action": ["Comedy", "Crime", "Thriller"],
	"Adventure": ["Biography", "Thriller", "War"],
	"Animation": ["Adventure", "Comedy", "Family", "Fantasy"],
	"Biography": ["Crime", "Mystery", "Sport"],
	"Comedy": ["Action", "Horror", "Romance"],
	"Crime": ["Drama", "Mystery", "Romance"],
	"Documentary": ["Biography", "Comedy", "Crime", "History"],
	"Drama": ["Romance", "Film-Noir", "Musical", "War"],
	"Family": ["Adventure", "Comedy", "Fantasy", "Romance"],
	"Fantasy": ["Adventure", "Comedy", "Drama", "Romance"],
	"Film-Noir": ["Crime", "Mystery", "Romance", "Thriller"],
	"History": ["Adventure", "Biography", "Drama", "War"],
	"Horror": ["Comedy", "Drama", "Sci-Fi"],
	"Music": ["Biography", "Documentary", "Drama"],
	"Musical": ["Comedy", "History", "Romance"],
	"Mystery": ["Adventure", "Comedy", "Thriller"],
	"Romance": ["Comedy", "Crime", "History", "Thriller"],
	"Sci-Fi": ["Animation", "Comedy", "Family", "Horror"],
	"Sport": ["Biography", "Comedy", "Documentary"],
	"Thriller": ["Comedy", "Crime", "Horror", "Mystery"],
	"War": ["Action", "Biography", "Comedy", "Documentary"],
	"Western": ["Action", "Adventure", "Comedy"]
}
```
##### TV Shows
```javascript
[
	"Action & Adventure",
	"Animation",
	"Beauty & Fashion",
	"Classic TV",
	"Comedy",
	"Documentary",
	"Drama",
	"Entertainment",
	"Family",
	"Food",
	"Gaming",
	"Health & Fitness",
	"Home & Garden",
	"Learning & Education",
	"Nature",
	"News",
	"Reality & Game Shows",
	"Science & Tech",
	"Science Fiction",
	"Soaps",
	"Sports",
	"Travel"
]
```
##### Music
```javascript 
[
	"Acoustic",
	"Alternative & Punk",
	"Blues",
	"Classical",
	"Country & Folk",
	"Dance & Electronic",
	"Easy Listening",
	"Gospel & Religious",
	"Hip Hop & Rap",
	"Holiday",
	"Instrumental",
	"Jazz",
	"Latin",
	"Metal",
	"Moods",
	"Other",
	"Pop",
	"R&B",
	"Rock",
	"Soundtrack",
	"World"
];
```

### Edit Artifact
```javascript
{  
    "oip-041":{  
        "editArtifact":{  
            "txid":"$artifactID",
            "timestamp":1234567890,
            "patch":{  
                "add":[  
                    {  
                        "path":"/payment/tokens/mtcproducer",
                        "value":""
                    }
                ],
                "replace":[  
                    {  
                        "path":"/storage/files/3/fname",
                        "value":"birthdayepFirst.jpg"
                    },
                    {  
                        "path":"/storage/files/3/dname",
                        "value":"Cover Art 2"
                    },
                    {  
                        "path":"/info/title",
                        "value":"Happy Birthday"
                    },
                    {  
                        "path":"/timestamp",
                        "value":1481420001
                    }
                ],
                "remove":[  
                    {  
                        "path":"/payment/tokens/mtmproducer"
                    },
                    {  
                        "path":"/storage/files/0/sugBuy"
                    }
                ]
            }
        }
    },
    "signature":"$txid-$MD5HashOfPatch-$timestamp"
}
```
### Transfer Artifact
```javascript
{  
    "oip-041":{  
        "transferArtifact":{  
            "txid":"$artifactID",
            "to":"$newPublisherAddress",
            "from":"$oldPublisherAddress",
            "timestamp":1234567890
        },
        "signature":"$artifactID-$newPublisherAddress-$oldPublisherAddress-$timestamp"
    }
}
```
### Deactivate Artifact
```javascript
{  
    "oip-041":{  
        "deactivateArtifact":{  
            "txid":"$artifactID",
            "timestamp":1234567890
        },
        "signature":"$txid-$publisher-$timestamp"
    }
}
```

### Multipart Data
You should not have to use the Multipart Data format, however should you need to reference it, here it is. When the JSON to be published is larger than 528 characters, the JSON gets split up into multiple parts. Each of these parts are then submitted as Transaction comments to the Florincoin Blockchain. Here is an example of an OIP 7 part artifact.

This data is formatted as follows:
```
alexandria-media-multipart($partNumber, $multipartArrayLength, $publisherAddress, $firstPartTXID, $signature):$choppedStringData
```
```
alexandria-media-multipart(0,6,FD6qwMcfpnsKmoL2kJSfp1czBMVicmkK1Q,0000000000000000000000000000000000000000000000000000000000000000,IBvdL1xJhvk2NIs7ckwsmK4hGGI2rnhgYwbTa6zy/FF1TxFyLuiv2fKTZYf7nmK0bHX0prUv4pl/CU/ZErvleW4=):{"oip-041":{"artifact":{"publisher":"FD6qwMcfpnsKmoL2kJSfp1czBMVicmkK1Q","timestamp":1481420000,"type":"music","info":{"title":"Happy Birthday EP","description":"this is the second organically grown, gluten free album released by Adam B. Levine - contact adam@tokenly.co
```
```
alexandria-media-multipart(1,6,FD6qwMcfpnsKmoL2kJSfp1czBMVicmkK1Q,5d0eb0bfb05815567717ec1d5b72c92c8bcf8d30c48785d6449970bb32a9c07b,IBnj6xxykNf3ZDpidg8dk4ioERFU3Gj2tKQ3dxFAXeIQB3gPibrWF5b4g4PIR8KimwqqmqDQ77PF4dApAhuXze4=):m with questions or comments or discuss collaborations.","year":"2016","extraInfo":{"artist":"Adam B. Levine","company":"","composers":["Adam B. Levine"],"copyright":"","usageProhibitions":"","usageRights":"","tags":[]}},"storage":{"network":"IPFS","location":"QmPukCZKe
```
```
alexandria-media-multipart(2,6,FD6qwMcfpnsKmoL2kJSfp1czBMVicmkK1Q,5d0eb0bfb05815567717ec1d5b72c92c8bcf8d30c48785d6449970bb32a9c07b,IMJbM7xMAVl/XWN0KpJiid/LADx+HdDNJUdiUkxm4JFyRKGCkF3VBt6cTUJ50YT3HO0heNMBCyh3HGFiunQWqis=):JD4KZFtstpvrguLaq94rsWfBxLU1QoZxvgRxA","files":[{"dname":"Skipping Stones","fame":"1 - Skipping Stones.mp3","fsize":6515667,"type":"album track","duration":1533.603293,"sugPlay":100,"minPlay":null,"sugBuy":750,"minBuy":500,"promo":10,"retail":15,"ptpFT":10,"ptpDT":20,"p
```
```
alexandria-media-multipart(3,6,FD6qwMcfpnsKmoL2kJSfp1czBMVicmkK1Q,5d0eb0bfb05815567717ec1d5b72c92c8bcf8d30c48785d6449970bb32a9c07b,IBdKG047JgK2XyWX86AFf9n1yT+QTtPJjgOnofP74wwBHZBYT4gJQeSNOfToIrerNkcXGr9zX+N1nTVhKLuscx0=):tpDA":50},{"dname":"Lessons","fame":"2 - Lessons with intro.mp3","fsize":6515667,"type":"album track","duration":1231.155243,"disallowPlay":1,"sugBuy":750,"minBuy":500,"promo":10,"retail":15,"ptpFT":10,"ptpDT":20,"ptpDA":50},{"dname":"Born to Roam","fame":"3 - Born to R
```
```
alexandria-media-multipart(4,6,FD6qwMcfpnsKmoL2kJSfp1czBMVicmkK1Q,5d0eb0bfb05815567717ec1d5b72c92c8bcf8d30c48785d6449970bb32a9c07b,H7KGidUTMG+6xBwudl1EXeFcBvGy9+UHnd9vrWC7ETTBCioioE0pphkozUgbZQx+jIldlEPMBnVuqox383P8nLI=):oam.mp3","fsize":6515667,"type":"album track","duration":2374.550714,"sugPlay":100,"minPlay":50,"disallowBuy":1,"promo":10,"retail":15,"ptpFT":10,"ptpDT":20,"ptpDA":50},{"dname":"Cover Art","fname":"birthdayepFINAL.jpg","type":"coverArt","disallowBuy":1}]},"payment":{"f
```
```
alexandria-media-multipart(5,6,FD6qwMcfpnsKmoL2kJSfp1czBMVicmkK1Q,5d0eb0bfb05815567717ec1d5b72c92c8bcf8d30c48785d6449970bb32a9c07b,INaPk7aMwksd9rzRXtCqND9RJYZPbUagosessK+b4D+JUfga/gT1gU25lvTs2hLZkcoqfVXGqlRsOrZ2agGYw3M=):iat":"USD","scale":"1000:1","sugTip":[5,50,100],"tokens":{"mtmcollector":"","mtmproducer":"","happybirthdayep":"","early":"","ltbcoin":"","btc":"1GMMg2J5iUKnDf5PbRr9TcKV3R6KfUiB55"}}},"signature":"H3XC/u9qz9pUP5g1+dyWUSR2euKFH3DWKd8hTdFINURvZvcdE7Q2hnNJa9QOuunCD1CPiVMOV
```
```
alexandria-media-multipart(6,6,FD6qwMcfpnsKmoL2kJSfp1czBMVicmkK1Q,5d0eb0bfb05815567717ec1d5b72c92c8bcf8d30c48785d6449970bb32a9c07b,HwRHpvyi99EM0xtA68FGLWJpd4sls/z6zNAjQh65OnQhRp19mSZNqoheYdw6a4QReUd0I0iBvMt0udgrIXLuE6Y=):q+8m+NcgMQTw60="}}
```
## License

This project uses the [MIT] License.



[TravisSVG]: https://travis-ci.org/oipwg/media-protocol.svg?branch=master
[TravisLink]: https://travis-ci.org/oipwg/media-protocol

[CoverallsSVG]: https://coveralls.io/repos/github/oipwg/media-protocol/badge.svg?branch=master
[CoverallsLink]: https://coveralls.io/github/oipwg/media-protocol?branch=master

[GoReportCardSVG]: https://goreportcard.com/badge/github.com/GuoxiW/media-protocol
[GoReportCardLink]: https://goreportcard.com/report/github.com/GuoxiW/media-protocol

[MIT]:LICENSE.md
