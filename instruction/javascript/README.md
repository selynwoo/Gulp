#Javascript 명령어 
 - `gulp-concat` (병합)
<br>

## gulp-concat (병합) 
**설치** <br>
- cmd : `npm i -D gulp-concat` 

**문법** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src(['./src/domheler-id.js', './src/domheler-tag.js'])
		.pipe(concat('combined.js'))
		.pipe(gulp.dest('./dist'));
});
```

