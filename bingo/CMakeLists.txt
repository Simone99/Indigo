if (BUILD_BINGO_POSTGRES OR BUILD_BINGO_ORACLE OR BUILD_BINGO_SQLSERVER)
    include(${CMAKE_CURRENT_SOURCE_DIR}/bingo-version.cmake)

    add_subdirectory(bingo-core)
    if (BUILD_BINGO_POSTGRES OR BUILD_BINGO_SQLSERVER)
        add_subdirectory(bingo-core-c)
    endif()
    if (BUILD_BINGO_POSTGRES)
        add_subdirectory(postgres)
    endif()
    if (BUILD_BINGO_ORACLE)
        add_subdirectory(oracle)
    endif()
    if (BUILD_BINGO_SQLSERVER)
        add_subdirectory(sqlserver)
    endif()
endif()

if (BUILD_BINGO_ELASTIC)
    add_subdirectory(bingo-elastic)
endif()
