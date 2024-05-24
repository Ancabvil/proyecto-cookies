# proyecto-cookies
## Selector de Idiomas
 
        String idioma="es";
        if (session.getAttribute("idioma") == null){
            session.setAttribute("idioma", "es");
            }else{
            idioma=(String)session.getAttribute("idioma");
            }
    session.setAttribute("idioma",request.getParameter("idioma"));
    response.sendRedirect("index.jsp");
 
## Serializado de carrito y método toString


  public Carrito(String contiene){
    if(contiene.length()>0){
        String[] deserializado = contiene.split("/");
        
        for (int i = 0; i < deserializado.length; i += 5) {
                int cantidad = Integer.parseInt(deserializado[i]);
                int codigo = Integer.parseInt(deserializado[i + 1]);
                String nombre = deserializado[i + 2];
                double precio = Double.parseDouble(deserializado[i + 3]);
                String imagen = deserializado[i + 4];

                Producto producto = new Producto(codigo, nombre, precio, imagen);
                ElementoDeCarrito elementoCarrito = new ElementoDeCarrito(producto, cantidad);

                elementos.add(elementoCarrito);

        @Override
  public String toString(){
      String catalogo="";
      for(ElementoDeCarrito recorrido: elementos){
          catalogo += recorrido.getCantidad()+
                  "/" + recorrido.getProducto().getCodigo()+ 
                  "/" + recorrido.getProducto().getNombre() + 
                  "/" + recorrido.getProducto().getPrecio() +
                  "/" + recorrido.getProducto().getImagen() +
                  "/";
      }
return catalogo;
}
## Clase compra con cookies
int codigo = Integer.parseInt(request.getParameter("codigo"));
  Cookie cookie = dameCookie(request, "carrito") ;
  Carrito carrito = new Carrito(cookie.getValue());
  carrito.meteProductoConCodigo(codigo);
  
  cookie = new Cookie("carrito", carrito.toString());
                cookie.setPath("/");
                cookie.setMaxAge(365 * 24 * 60 * 60);
                response.addCookie(cookie);
  
    
  response.sendRedirect("index.jsp");
    public static Cookie dameCookie(HttpServletRequest request, String nombre) {
        Cookie[] cookies = request.getCookies();
            if (cookies != null) {
               for (Cookie cookie : cookies) {
                   if (cookie.getName().equals(nombre)) {
                       return cookie;
                      }
                }
            }
            return null;
        }

