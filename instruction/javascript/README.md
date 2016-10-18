#Javascript 명령어 
- `gulp-concat` (병합)
- `gulp-uglify` (병합)
<br>

## gulp-concat (병합) 
- **설치** <br>
- cmd : `npm i -D gulp-concat` 

- **Modules 호출**
```md
var gulp = require('gulp'),
    concat = require('gulp-concat');
```

- **지정한 js 병합** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src(['./src/domheler-id.js', './src/domheler-tag.js'])
		.pipe(concat('combined.js'))
		.pipe(gulp.dest('./dist'));
});
```

- **모든 js 병합** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src('./src/*.js') 
		.pipe(concat('combined.js'))
		.pipe(gulp.dest('./dist'));
});
```

- **특정파일 우선적 병합** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src(['./src/domhelper-prevEl.js', './src/*.js']) 
		.pipe(concat('combined.js'))
		.pipe(gulp.dest('./dist'));
});
```

- **하위디렉터리 모든 js 병합** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src('src/js/libs/**/*.js') //src 디렉터리의 js/libs 하위 디렉터리를 생성 후 실행 후 확인
		.pipe(concat('combined.js'))
		.pipe(gulp.dest('./dist'));
});
```

