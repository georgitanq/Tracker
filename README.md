# Tracker
using System;
using System.Collections.Generic;
using System.Windows.Forms;

namespace ActivityTracker
{
    public partial class Form1 : Form
    {
        // Списък за съхраняване на тренировките
        private List<Activity> activities = new List<Activity>();

        public Form1()
        {
            InitializeComponent();
            // Инициализация на ComboBox с различни видове тренировки
            cmbExerciseType.Items.AddRange(new string[] { "Бягане", "Плуване", "Колоездене", "Йога", "Тежести" });
            cmbExerciseType.SelectedIndex = 0; // Избиране на първия елемент по подразбиране
        }

        // Клас за съхраняване на данни за тренировка
        public class Activity
        {
            public string ExerciseType { get; set; }
            public double Duration { get; set; } // Време в минути
            public double CaloriesBurned { get; set; }
        }

        private void btnAddActivity_Click(object sender, EventArgs e)
        {
            try
            {
                // Вземане на входните стойности
                string exerciseType = cmbExerciseType.SelectedItem.ToString();
                double duration = double.Parse(txtDuration.Text); // Времето на тренировката в минути
                double calories = double.Parse(txtCalories.Text); // Изгорените калории

                // Създаване на нова тренировка
                Activity newActivity = new Activity()
                {
                    ExerciseType = exerciseType,
                    Duration = duration,
                    CaloriesBurned = calories
                };

                // Добавяне на тренировката в списъка
                activities.Add(newActivity);

                // Добавяне на тренировката към ListBox-а
                lstActivities.Items.Add($"{exerciseType}: {duration} минути, {calories} калории");

                // Изчистване на полетата за въвеждане
                txtDuration.Clear();
                txtCalories.Clear();
            }
            catch (FormatException)
            {
                MessageBox.Show("Моля, въведете валидни стойности за време и калории.");
            }
        }

        private void btnClearList_Click(object sender, EventArgs e)
        {
            // Изчистване на всички тренировки
            activities.Clear();
            lstActivities.Items.Clear();
        }
    }
}
