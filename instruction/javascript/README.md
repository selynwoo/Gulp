#Javascript 명령어 
 - `gulp-concat` (병합)
<br>

## gulp-concat (병합) 
**설치** <br>
- cmd : `npm i -D gulp-concat` 

**지정한 js 병합** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src(['./src/domheler-id.js', './src/domheler-tag.js'])
		.pipe(concat('combined.js'))
		.pipe(gulp.dest('./dist'));
});
```

**모든 js 병합** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src('./src/*.js') 
		.pipe(concat('combined.js'))
		.pipe(gulp.dest('./dist'));
});
```

**특정파일 우선적으로 병합** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src(['./src/domhelper-prevEl.js', './src/*.js']) 
		.pipe(concat('combined.js'))
		.pipe(gulp.dest('./dist'));
});
```

