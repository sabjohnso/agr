

MACRO( ADD_CXX_BINDING name )
  ADD_CUSTOM_COMMAND( 
    OUTPUT ${name}.hpp
    OUTPUT ${name}.cpp
    COMMAND xsdcxx cxx-tree --generate-serialization --generate-ostream ${name}.xsd
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
    MAIN_DEPENDENCY ${CMAKE_CURRENT_BINARY_DIR}/${name}.xsd )
  TARGET_LINK_LIBRARY( cxx${name} xerces )
ENDMACRO( ADD_CXX_BINDING )


ADD_LIBRARY( cxx${name} SHARED ${name}.cpp ${name}.hpp )


MACRO( ADD_PYTHON_BINDING name )
  ADD_CUSTOM_COMMAND(
    OUTPUT py${name}.py
    COMMAND pyxbgen -u ${name}.xsd
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR})
ENDMACRO( ADD_PYTHON_BINDING )

ADD_CUSTOM_COMMAND(
  OUTPUT gx.xsd
  wget http://www.gedcomx.org/gx.xsd
  WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR})



