# MNIST-Fortran-Binary-Format
Convert MNIST database to Fortran binary formats for ease of use.

训练集和测试集的图片数据都已经压缩成ZIP格式，需要先解压。
解压之后可以得到四个文件：
- train-images.fortran
- t10k-images.fortran
- train-labels.fortran
- t10k-labels.fortran

train-images.fortran和t10k-images.fortran可以使用类似于下述方式读取：

```fortran
PROGRAM MAIN
implicit none    
    
    integer(kind=4) :: magic_number, sample_count, row, col, point_count
    integer(kind=4) :: pixel
    integer :: i
    
    open(UNIT=30, FILE='train-images.fortran', &
        ACCESS='stream', FORM='unformatted', STATUS='old')
    read(30) magic_number, sample_count, row, col
    
    point_count = row*col*sample_count
    
    do i=1, point_count
        read(30) pixel       
    end do
    
    close(30)
    
END PROGRAM
```

train-labels.fortran和t10k-labels.fortran可以使用类似于下述方式读取：

```fortran
PROGRAM MAIN
implicit none    
    
    integer(kind=4) :: magic_number, sample_count
    integer(kind=4) :: label
    integer :: i
    
    open(UNIT=30, FILE='train-labels.fortran', &
        ACCESS='stream', FORM='unformatted', STATUS='old')
    read(30) magic_number, sample_count
    
    do i=1, sample_count
        read(30) label       
    end do
    
    close(30)
    
END PROGRAM
```
