# Count per grade and compute percentage
total = df_filtered.count()

grade_dist = df_filtered.groupBy("grade") \
    .agg(F.count("student_id").alias("count")) \
    .withColumn("percentage", F.round((F.col("count") / total) * 100, 2)) \
    .orderBy("grade")

grade_dist.show()
