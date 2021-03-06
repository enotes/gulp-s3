# @enotes/gulp-s3

> s3 plugin for [gulp](https://github.com/wearefractal/gulp)

## Usage

First, install `@enotes/gulp-s3` as a development dependency:

```shell
npm i --save-dev git+ssh://git@github.com:enotes/gulp-s3.git#v0.4.2
```

Setup your aws.json file
```javascript
{
  "key": "AKIAI3Z7CUAFHG53DMJA",
  "secret": "acYxWRu5RRa6CwzQuhdXEfTpbQA+1XQJ7Z1bGTCx",
  "bucket": "dev.example.com",
  "region": "eu-west-1"
}
```

Then, use it in your `gulpfile.js`:
```javascript
const s3 = require("@enotes/gulp-s3");

aws = JSON.parse(fs.readFileSync('./aws.json'));
gulp.src("./dist/**")
    .pipe(s3(aws));
```

## API


#### options.headers

Type: `Array`          
Default: `[]`

Headers to set to each file uploaded to S3

```javascript
const options = { headers: {"Cache-Control": "max-age=315360000, no-transform, public"} }
gulp.src("./dist/**", {read: false})
    .pipe(s3(aws, options));
```

#### options.gzippedOnly

Type: `Boolean`          
Default: `false`

Only upload files with .gz extension, additionally it will remove the .gz suffix on destination filename and set appropriate Content-Type and Content-Encoding headers.

```javascript
const gulp = require("gulp");
const s3 = require("@enotes/gulp-s3");
const gzip = require("gulp-gzip");
const options = { gzippedOnly: true };

gulp.src("./dist/**")
    .pipe(gzip())
    .pipe(s3(aws, options));

});
```

#### options.maxRetries

Type: `Number`         
Default: [3][Intimidate]

The number of times to retry before failing.

```javascript
const gulp = require("gulp");
const s3 = require("@enotes/gulp-s3");
const options = { maxRetries: 5 };

gulp.src("./dist/**")
    .pipe(s3(aws, options));
```

## License

[MIT License](http://en.wikipedia.org/wiki/MIT_License)
[Intimidate]: https://github.com/jergason/intimidate#api
