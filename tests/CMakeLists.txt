set(tstName read_nemsio)
set(srcName read_nemsio.f90)
set(exeName read_nemsio.x)

execute_process(COMMAND ${CMAKE_COMMAND} -E create_symlink
                ${CMAKE_CURRENT_SOURCE_DIR}/testdataset
                ${CMAKE_CURRENT_BINARY_DIR}/testdataset)

add_executable(${exeName} ${srcName})
add_dependencies(${exeName} nemsio)
target_link_libraries( ${exeName} PUBLIC nemsio bacio::bacio_4 w3nco::w3nco_d)
add_test(NAME ${tstName} COMMAND ${exeName} testdataset)

add_pfunit_ctest (nemsio_test
  TEST_SOURCES test_mod.pf
  LINK_LIBRARIES nemsio bacio::bacio_4 w3nco::w3nco_d
)
