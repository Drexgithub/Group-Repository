# Check total row count
total_rows = df.count()
print(f"Total rows: {total_rows}")

# Check missing/null values per column
print("=== Missing Values ===")
df.select([
    F.count(F.when(F.col(c).isNull(), c)).alias(c)
    for c in df.columns
]).show()

# Check for invalid records
invalid_score = df.filter(F.col("total_score") > 100).count()
invalid_hours = df.filter(F.col("weekly_self_study_hours") < 0).count()

print(f"Scores above 100 (invalid): {invalid_score}")
print(f"Negative study hours (invalid): {invalid_hours}")
