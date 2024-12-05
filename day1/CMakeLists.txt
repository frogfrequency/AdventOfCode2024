#[===[ LIBRARY ]===]
 
add_library("day1Lib"
    "lib/day1.cpp"
)
 
target_include_directories("day1Lib" PUBLIC "lib" )
 
#[===[ TESTS ]===]
 
add_executable("day1Tests"
    "test/day1Tests.cpp"
)
 
target_link_libraries("day1Tests" PRIVATE
    "day1Lib"
    "Catch2::Catch2WithMain"
)
 
add_test(NAME "day1Tests" COMMAND "day1Tests")
 
#[===[ APPLICATION ]===]
 
add_executable("day1App"
    "app/main.cpp"
)
 
target_link_libraries("day1App" PRIVATE
    "day1Lib"
)