makeCacheMatrix
===============

funcion
##Sandy Ceracapa

## El cache funciona de una manera similar a como lo hace la memoria principal (RAM), 
##pero es de menor tamaño y de acceso más rápido. 
##Es usado por la unidad central de procesamiento para reducir el tiempo 
##de acceso a datos ubicados en la memoria principal que se utilizan con más frecuencia.
##makeCacheMatrix : Esta función crea un objeto especial "matriz " 
##que se puede almacenar en caché su inversa .


## se debera crear una  matriz cuadrada invertible como por ejemplo 
## x<-matrix(c(1,1,0,1,0,1,0,1,0),3,3) 

makeCacheMatrix <- function(x = matrix()) {
  i  <- NULL
  set  <- function(y){
    x <<- y
    i <<- NULL 
  }
  get  <- function() x
  setinverse  <- function(inverse) i  <<- inverse
  getinverse  <- function() i
  list(set= set, get = get, 
       setinverse = setinverse, 
       getinverse = getinverse)
}


##cacheSolve : Esta función calcula la inversa de la " matriz " especial devuelto
##por makeCacheMatrix anteriormente. Si la inversa ya se ha calculado ( y la matriz
##no ha cambiado ) , entonces el cachesolve debe recuperar la inversa de la memoria caché .

cacheSolve <- function(x, ...) {
  i  <- x$getinverse()
  if (!is.null(i)){
    message("getting cached data")
    return(i)
  }
  data  <- x$get()
  i  <- solve(data, ...)
  x$setinverse(i)
  i
}
