if (NETGEN_USE_PYTHON)
  find_package(Sphinx)
  if(SPHINX_FOUND)
    # configured documentation tools and intermediate build results
    set(BINARY_BUILD_DIR "${CMAKE_CURRENT_BINARY_DIR}/_build")

    # Sphinx cache with pickled ReST documents
    set(SPHINX_CACHE_DIR "${CMAKE_CURRENT_BINARY_DIR}/_doctrees")

    # HTML output directory
    set(SPHINX_OUTPUT_DIR "${CMAKE_CURRENT_BINARY_DIR}")

    configure_file(
      "${CMAKE_CURRENT_SOURCE_DIR}/conf.py"
      "${BINARY_BUILD_DIR}/conf.py"
      @ONLY)

    add_custom_target(docs
      ${CMAKE_COMMAND} -E env NETGEN_DOCUMENTATION_RST_FORMAT=1
      ${SPHINX_EXECUTABLE}
      -a -q -b html
      -c "${BINARY_BUILD_DIR}"
      -d "${SPHINX_CACHE_DIR}"
      "${CMAKE_CURRENT_SOURCE_DIR}"
      "${SPHINX_OUTPUT_DIR}/html"
      COMMENT "Building HTML documentation with Sphinx"
      )

      add_custom_target(docs_latex
      ${CMAKE_COMMAND} -E env NETGEN_DOCUMENTATION_RST_FORMAT=1
    	${SPHINX_EXECUTABLE}
    	-q -b latex
    	-c "${BINARY_BUILD_DIR}"
    	-d "${SPHINX_CACHE_DIR}"
    	"${CMAKE_CURRENT_SOURCE_DIR}"
    	"${SPHINX_OUTPUT_DIR}/latex"
    	COMMENT "Building Latex documentation with Sphinx")


    message("Sphinx found, you can build the documentation with make docu")
  else(SPHINX_FOUND)
    message("Sphinx not found, if you want to build the documentation you have to install Sphinx")
  endif(SPHINX_FOUND)

endif(NETGEN_USE_PYTHON)
