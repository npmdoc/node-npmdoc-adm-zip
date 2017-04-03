# api documentation for  [adm-zip (v0.4.7)](http://github.com/cthackers/adm-zip)  [![npm package](https://img.shields.io/npm/v/npmdoc-adm-zip.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-adm-zip) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-adm-zip.svg)](https://travis-ci.org/npmdoc/node-npmdoc-adm-zip)
#### A Javascript implementation of zip for nodejs. Allows user to create or extract zip files both in memory or to/from disk

[![NPM](https://nodei.co/npm/adm-zip.png?downloads=true)](https://www.npmjs.com/package/adm-zip)

[![apidoc](https://npmdoc.github.io/node-npmdoc-adm-zip/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-adm-zip_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-adm-zip/build..beta..travis-ci.org/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-adm-zip/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-adm-zip/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Nasca Iacob",
        "email": "sy@another-d-mention.ro",
        "url": "https://github.com/cthackers"
    },
    "bugs": {
        "url": "https://github.com/cthackers/adm-zip/issues",
        "email": "sy@another-d-mention.ro"
    },
    "dependencies": {},
    "description": "A Javascript implementation of zip for nodejs. Allows user to create or extract zip files both in memory or to/from disk",
    "devDependencies": {},
    "directories": {},
    "dist": {
        "shasum": "8606c2cbf1c426ce8c8ec00174447fd49b6eafc1",
        "tarball": "https://registry.npmjs.org/adm-zip/-/adm-zip-0.4.7.tgz"
    },
    "engines": {
        "node": ">=0.3.0"
    },
    "files": [
        "adm-zip.js",
        "headers",
        "methods",
        "util",
        "zipEntry.js",
        "zipFile.js"
    ],
    "gitHead": "6708a3e5788ff9e67ddba288397f7788a5c02855",
    "homepage": "http://github.com/cthackers/adm-zip",
    "keywords": [
        "zip",
        "methods",
        "archive",
        "unzip"
    ],
    "licenses": [
        {
            "type": "MIT",
            "url": "https://raw.github.com/cthackers/adm-zip/master/MIT-LICENSE.txt"
        }
    ],
    "main": "adm-zip.js",
    "maintainers": [
        {
            "name": "cthackers",
            "email": "sy@another-d-mention.ro"
        }
    ],
    "name": "adm-zip",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/cthackers/adm-zip.git"
    },
    "scripts": {},
    "version": "0.4.7"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module adm-zip](#apidoc.module.adm-zip)
1.  object <span class="apidocSignatureSpan">adm-zip.</span>utils

#### [module adm-zip.utils](#apidoc.module.adm-zip.utils)
1.  [function <span class="apidocSignatureSpan">adm-zip.utils.</span>FileAttr (path)](#apidoc.element.adm-zip.utils.FileAttr)
1.  [function <span class="apidocSignatureSpan">adm-zip.utils.</span>crc32 (buf)](#apidoc.element.adm-zip.utils.crc32)
1.  [function <span class="apidocSignatureSpan">adm-zip.utils.</span>findFiles (path)](#apidoc.element.adm-zip.utils.findFiles)
1.  [function <span class="apidocSignatureSpan">adm-zip.utils.</span>getAttributes (path)](#apidoc.element.adm-zip.utils.getAttributes)
1.  [function <span class="apidocSignatureSpan">adm-zip.utils.</span>makeDir (path)](#apidoc.element.adm-zip.utils.makeDir)
1.  [function <span class="apidocSignatureSpan">adm-zip.utils.</span>methodToString (method)](#apidoc.element.adm-zip.utils.methodToString)
1.  [function <span class="apidocSignatureSpan">adm-zip.utils.</span>setAttributes (path)](#apidoc.element.adm-zip.utils.setAttributes)
1.  [function <span class="apidocSignatureSpan">adm-zip.utils.</span>toBuffer (input)](#apidoc.element.adm-zip.utils.toBuffer)
1.  [function <span class="apidocSignatureSpan">adm-zip.utils.</span>writeFileTo (path, content, overwrite, attr)](#apidoc.element.adm-zip.utils.writeFileTo)
1.  [function <span class="apidocSignatureSpan">adm-zip.utils.</span>writeFileToAsync (path, content, overwrite, attr, callback)](#apidoc.element.adm-zip.utils.writeFileToAsync)
1.  object <span class="apidocSignatureSpan">adm-zip.utils.</span>Constants
1.  object <span class="apidocSignatureSpan">adm-zip.utils.</span>Errors



# <a name="apidoc.module.adm-zip"></a>[module adm-zip](#apidoc.module.adm-zip)



# <a name="apidoc.module.adm-zip.utils"></a>[module adm-zip.utils](#apidoc.module.adm-zip.utils)

#### <a name="apidoc.element.adm-zip.utils.FileAttr"></a>[function <span class="apidocSignatureSpan">adm-zip.utils.</span>FileAttr (path)](#apidoc.element.adm-zip.utils.FileAttr)
- description and source-code
```javascript
FileAttr = function (path) {

    var _path = path || "",
        _permissions = 0,
        _obj = newAttr(),
        _stat = null;

    function newAttr() {
        return {
            directory : false,
            readonly : false,
            hidden : false,
            executable : false,
            mtime : 0,
            atime : 0
        }
    }

    if (_path && fs.existsSync(_path)) {
        _stat = fs.statSync(_path);
        _obj.directory = _stat.isDirectory();
        _obj.mtime = _stat.mtime;
        _obj.atime = _stat.atime;
        _obj.executable = !!(1 & parseInt ((_stat.mode & parseInt ("777", 8)).toString (8)[0]));
        _obj.readonly = !!(2 & parseInt ((_stat.mode & parseInt ("777", 8)).toString (8)[0]));
        _obj.hidden = pth.basename(_path)[0] === ".";
    } else {
        console.warn("Invalid path: " + _path)
    }

    return {

        get directory () {
            return _obj.directory;
        },

        get readOnly () {
            return _obj.readonly;
        },

        get hidden () {
            return _obj.hidden;
        },

        get mtime () {
            return _obj.mtime;
        },

        get atime () {
           return _obj.atime;
        },


        get executable () {
            return _obj.executable;
        },

        decodeAttributes : function(val) {

        },

        encodeAttributes : function (val) {

        },

        toString : function() {
           return '{\n' +
               '\t"path" : "' + _path + ",\n" +
               '\t"isDirectory" : ' + _obj.directory + ",\n" +
               '\t"isReadOnly" : ' + _obj.readonly + ",\n" +
               '\t"isHidden" : ' + _obj.hidden + ",\n" +
               '\t"isExecutable" : ' + _obj.executable + ",\n" +
               '\t"mTime" : ' + _obj.mtime + "\n" +
               '\t"aTime" : ' + _obj.atime + "\n" +
           '}';
        }
    }

}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.adm-zip.utils.crc32"></a>[function <span class="apidocSignatureSpan">adm-zip.utils.</span>crc32 (buf)](#apidoc.element.adm-zip.utils.crc32)
- description and source-code
```javascript
crc32 = function (buf) {
    var b = new Buffer(4);
    if (!crcTable.length) {
        for (var n = 0; n < 256; n++) {
            var c = n;
            for (var k = 8; --k >= 0;)  //
                if ((c & 1) != 0)  { c = 0xedb88320 ^ (c >>> 1); } else { c = c >>> 1; }
            if (c < 0) {
                b.writeInt32LE(c, 0);
                c = b.readUInt32LE(0);
            }
            crcTable[n] = c;
        }
    }
    var crc = 0, off = 0, len = buf.length, c1 = ~crc;
    while(--len >= 0) c1 = crcTable[(c1 ^ buf[off++]) & 0xff] ^ (c1 >>> 8);
    crc = ~c1;
    b.writeInt32LE(crc & 0xffffffff, 0);
    return b.readUInt32LE(0);
}
```
- example usage
```shell
...
    _entryHeader.loadDataHeaderFromBinary(input);
    return input.slice(_entryHeader.realDataOffset, _entryHeader.realDataOffset + _entryHeader.compressedSize)
}

function crc32OK(data) {
    // if bit 3 (0x08) of the general-purpose flags field is set, then the CRC-32 and file sizes are not known when the header is
 written
    if (_entryHeader.flags & 0x8 != 0x8) {
       if (Utils.crc32(data) != _entryHeader.crc) {
           return false;
       }
    } else {
        // @TODO: load and check data descriptor header
        // The fields in the local header are filled with zero, and the CRC-32 and size are appended in a 12-byte structure
        // (optionally preceded by a 4-byte signature) immediately after the compressed data:
    }
...
```

#### <a name="apidoc.element.adm-zip.utils.findFiles"></a>[function <span class="apidocSignatureSpan">adm-zip.utils.</span>findFiles (path)](#apidoc.element.adm-zip.utils.findFiles)
- description and source-code
```javascript
findFiles = function (path) {
    return findSync(path, true);
}
```
- example usage
```shell
...
			localPath = localPath.split("\\").join("/"); //windows fix
            localPath = pth.normalize(localPath);
            if (localPath.charAt(localPath.length - 1) != "/")
                localPath += "/";

            if (fs.existsSync(localPath)) {

                var items = Utils.findFiles(localPath),
                    self = this;

                if (items.length) {
                    items.forEach(function(path) {
						var p = path.split("\\").join("/").replace( new RegExp(localPath, 'i'), ""); //windows fix
if (filter(p)) {
    if (p.charAt(p.length - 1) !== "/") {
...
```

#### <a name="apidoc.element.adm-zip.utils.getAttributes"></a>[function <span class="apidocSignatureSpan">adm-zip.utils.</span>getAttributes (path)](#apidoc.element.adm-zip.utils.getAttributes)
- description and source-code
```javascript
getAttributes = function (path) {

}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.adm-zip.utils.makeDir"></a>[function <span class="apidocSignatureSpan">adm-zip.utils.</span>makeDir (path)](#apidoc.element.adm-zip.utils.makeDir)
- description and source-code
```javascript
makeDir = function (path) {
    mkdirSync(path);
}
```
- example usage
```shell
...
overwrite = overwrite || false;
if (!_zip) {
    throw Utils.Errors.NO_ZIP;
}

_zip.entries.forEach(function(entry) {
    if (entry.isDirectory) {
        Utils.makeDir(pth.resolve(targetPath, entry.entryName.toString()));
        return;
    }
    var content = entry.getData();
    if (!content) {
        throw Utils.Errors.CANT_EXTRACT_FILE + "2";
    }
    Utils.writeFileTo(pth.resolve(targetPath, entry.entryName.toString()), content, overwrite);
...
```

#### <a name="apidoc.element.adm-zip.utils.methodToString"></a>[function <span class="apidocSignatureSpan">adm-zip.utils.</span>methodToString (method)](#apidoc.element.adm-zip.utils.methodToString)
- description and source-code
```javascript
methodToString = function (method) {
    switch (method) {
        case Constants.STORED:
            return 'STORED (' + method + ')';
        case Constants.DEFLATED:
            return 'DEFLATED (' + method + ')';
        default:
            return 'UNSUPPORTED (' + method + ')';
    }

}
```
- example usage
```shell
...
},

toString : function() {
    return '{\n' +
        '\t"made" : ' + _verMade + ",\n" +
        '\t"version" : ' + _version + ",\n" +
        '\t"flags" : ' + _flags + ",\n" +
        '\t"method" : ' + Utils.methodToString(_method) + ",\n" +
        '\t"time" : ' + _time + ",\n" +
        '\t"crc" : 0x' + _crc.toString(16).toUpperCase() + ",\n" +
        '\t"compressedSize" : ' + _compressedSize + " bytes,\n" +
        '\t"size" : ' + _size + " bytes,\n" +
        '\t"fileNameLength" : ' + _fnameLen + ",\n" +
        '\t"extraLength" : ' + _extraLen + " bytes,\n" +
        '\t"commentLength" : ' + _comLen + " bytes,\n" +
...
```

#### <a name="apidoc.element.adm-zip.utils.setAttributes"></a>[function <span class="apidocSignatureSpan">adm-zip.utils.</span>setAttributes (path)](#apidoc.element.adm-zip.utils.setAttributes)
- description and source-code
```javascript
setAttributes = function (path) {

}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.adm-zip.utils.toBuffer"></a>[function <span class="apidocSignatureSpan">adm-zip.utils.</span>toBuffer (input)](#apidoc.element.adm-zip.utils.toBuffer)
- description and source-code
```javascript
toBuffer = function (input) {
    if (Buffer.isBuffer(input)) {
        return input;
    } else {
        if (input.length == 0) {
            return new Buffer(0)
        }
        return new Buffer(input, 'utf8');
    }
}
```
- example usage
```shell
...
	var zip = new AdmZip();
	
	// add file directly
	zip.addFile("test.txt", new Buffer("inner content of the file"), "entry comment goes here");
	// add local file
	zip.addLocalFile("/home/me/some_picture.png");
	// get everything as a buffer
	var willSendthis = zip.toBuffer();
	// or write everything to disk
	zip.writeZip(/*target file name*/"/home/me/files.zip");
	
	
	// ... more examples in the wiki
'''
...
```

#### <a name="apidoc.element.adm-zip.utils.writeFileTo"></a>[function <span class="apidocSignatureSpan">adm-zip.utils.</span>writeFileTo (path, content, overwrite, attr)](#apidoc.element.adm-zip.utils.writeFileTo)
- description and source-code
```javascript
writeFileTo = function (path, content, overwrite, attr) {
    if (fs.existsSync(path)) {
        if (!overwrite)
            return false; // cannot overwite

        var stat = fs.statSync(path);
        if (stat.isDirectory()) {
            return false;
        }
    }
    var folder = pth.dirname(path);
    if (!fs.existsSync(folder)) {
        mkdirSync(folder);
    }

    var fd;
    try {
        fd = fs.openSync(path, 'w', 438); // 0666
    } catch(e) {
        fs.chmodSync(path, 438);
        fd = fs.openSync(path, 'w', 438);
    }
    if (fd) {
        fs.writeSync(fd, content, 0, content.length, 0);
        fs.closeSync(fd);
    }
    fs.chmodSync(path, attr || 438);
    return true;
}
```
- example usage
```shell
...
    var children = _zip.getEntryChildren(item);
    children.forEach(function(child) {
        if (child.isDirectory) return;
        var content = child.getData();
        if (!content) {
            throw Utils.Errors.CANT_EXTRACT_FILE;
        }
        Utils.writeFileTo(pth.resolve(targetPath, maintainEntryPath ? child.entryName : child.entryName.substr(item.entryName.length
)), content, overwrite);
    });
    return true;
}

var content = item.getData();
if (!content) throw Utils.Errors.CANT_EXTRACT_FILE;
...
```

#### <a name="apidoc.element.adm-zip.utils.writeFileToAsync"></a>[function <span class="apidocSignatureSpan">adm-zip.utils.</span>writeFileToAsync (path, content, overwrite, attr, callback)](#apidoc.element.adm-zip.utils.writeFileToAsync)
- description and source-code
```javascript
writeFileToAsync = function (path, content, overwrite, attr, callback) {
    if(typeof attr === 'function') {
        callback = attr;
        attr = undefined;
    }

    fs.exists(path, function(exists) {
        if(exists && !overwrite)
            return callback(false);

        fs.stat(path, function(err, stat) {
            if(exists &&stat.isDirectory()) {
                return callback(false);
            }

            var folder = pth.dirname(path);
            fs.exists(folder, function(exists) {
                if(!exists)
                    mkdirSync(folder);

                fs.open(path, 'w', 438, function(err, fd) {
                    if(err) {
                        fs.chmod(path, 438, function(err) {
                            fs.open(path, 'w', 438, function(err, fd) {
                                fs.write(fd, content, 0, content.length, 0, function(err, written, buffer) {
                                    fs.close(fd, function(err) {
                                        fs.chmod(path, attr || 438, function() {
                                            callback(true);
                                        })
                                    });
                                });
                            });
                        })
                    } else {
                        if(fd) {
                            fs.write(fd, content, 0, content.length, 0, function(err, written, buffer) {
                                fs.close(fd, function(err) {
                                    fs.chmod(path, attr || 438, function() {
                                        callback(true);
                                    })
                                });
                            });
                        } else {
                            fs.chmod(path, attr || 438, function() {
                                callback(true);
                            })
                        }
                    }
                });
            })
        })
    })
}
```
- example usage
```shell
...
                entry.getDataAsync(function(content) {
                    if(i <= 0) return;
                    if (!content) {
i = 0;
callback(new Error(Utils.Errors.CANT_EXTRACT_FILE + "2"));
return;
                    }
                    Utils.writeFileToAsync(pth.resolve(targetPath, entry.entryName.toString()), content, overwrite, function(succ
) {
if(i <= 0) return;

if(!succ) {
    i = 0;
    callback(new Error('Unable to write'));
    return;
}
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
