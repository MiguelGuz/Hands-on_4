analisis y razonamiento sobre las conductas de consumo de los clientes.

// definir la estructura de los clientes, tarjetas y los productos en el catálogo.

(deftemplate cliente (slot id (type INTEGER)) (slot nombre (type STRING)) (slot correo (type STRING)) (slot telefono (type STRING)))

(deftemplate tarjeta (slot nombre (type STRING)) (slot tasa (type FLOAT)) (slot limite (type FLOAT)))

(deftemplate C_producto (slot marca (type STRING)) (slot modelo (type STRING)) (slot memoria (type INTEGER)) (slot precio (type FLOAT)) (slot existencia (type INTEGER)))

// definir datos y reglas del negocio (ademas de reflejar las compras en el catalogo)

(defrule agregar-cliente (not (cliente (id ?))) => 
(assert (cliente (id 1) (nombre "saul fernando") (correo "fenando2289@gmail.com") (cel "3311223344")))
(assert (cliente (id 2) (nombre "adali adamari") (correo "adamari_232@gmail.com") (cel "3399887766"))) 
(assert (cliente (id 3) (nombre "john chon") (correo "jhon_chon117@hotmail.com") (cel "3311778822"))))

defrule agregar-tarjetas (not (tarjeta (nombre ?))) => 
(assert (tarjeta (nombre "Banamex") (tasa 20.0) (limite 50000.0))) 
(assert (tarjeta (nombre "Liverpool VISA") (tasa 18.0) (limite 70000.0))) 
(assert (tarjeta (nombre "contado") (tasa 0) (limite 0))) 
(assert (tarjeta (nombre "American Express") (tasa 25.0) (limite 100000.0))))

(defrule agregar-productos (not (producto (marca ?))) =>
(assert (producto (marca "Apple") (modelo "Watch Series 6") (memoria 32) (precio 7999.99) (existencia 10))) 
(assert (producto (marca "apple") (modelo "iPhone 14") (memoria 128) (precio 16999.99) (existencia 9))) 
(assert (producto (marca "samsung") (modelo "tablet SamsungX") (memoria 256) (precio 10999.99) (existencia 8))) 
(assert (producto (marca "apple") (modelo "AppleWatch") (memoria 64) (precio 12999.99) (existencia 16))) 
(assert (producto (marca "samsung") (modelo "Smartphone") (memoria 128) (precio 8999.99) (existencia 3))))


(defrule oferta-iphone14-banamex (buy cliente (producto (modelo "iPhone 14")) (tarjeta (nombre "Banamex"))) =>
(assert (offer cliente"24 meses sin intereses en iPhone 14 con Banamex")))

(defrule oferta-tablet-samsung (buy cliente (producto (modelo "Tablet SamsungX")) (tarjeta (name "Liverpool VISA")))=>
 (assert (offer cliente "12 meses sin intereses en Tablet SamsungX con Liverpool VISA")))

(defrule oferta-applewatch-iphone14(buy cliente (producto(modelo "AppleWatch")) (producto (modelo "iPhone 14")) (tarjeta (nombre "Contado")))=>
  (assert (offer cliente "100 pesos en vales por cada 1000 pesos de compra en AppleWatch e iPhone14 al contado")))

(defrule oferta-smartphone-funda-mica(buy cliente (producto (modelo "Smartphone")))=>
(assert (offer cliente "Funda y mica con 15% de descuento en Smartphone")))

(defrule reflejar-compra-en-catalogo producto <- (producto (modelo) (existencia))
  (buy cliente (producto (modelo)))
  (test (>= existencia 1)) =>  (modify producto (existencia (- existencia 1))))
  
// la agregacion y prueba de input y output no fue posible (ademas de tener que subir el formato de trabajo asi (desconociendo si es la manera correcta de subir el trabo))
// ya que mi equipo de trabajo escolar se vio con unas fallas y tuve que trabajar en una computadora ajena sin poder descargar los recursos para las actividades 
